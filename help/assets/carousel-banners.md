---
title: Banner a carosello
description: Scoprite come utilizzare i banner carosello in Dynamic Media
uuid: 73684a08-d84d-4665-ab89-3a1bf88ac5dd
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e26c7f7f-bdd7-421a-8614-ba48abf381d2
docset: aem65
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '4814'
ht-degree: 5%

---


# Banner a carosello{#carousel-banners}

I banner carosello consentono agli esperti di marketing di promuovere la conversione creando facilmente contenuti promozionali interattivi a rotazione e distribuendoli su qualsiasi schermo.

La creazione e la modifica dei contenuti contenuti contenuti nei banner promozionali può richiedere molto tempo, limitando la possibilità di pubblicare rapidamente nuovi contenuti o rendendoli più mirati. I banner carosello consentono di creare o modificare rapidamente i banner a rotazione, aggiungere interattività quali punti di attivazione collegati ai dettagli del prodotto o alle risorse correlate e distribuirli su qualsiasi schermo, consentendo di immettere più rapidamente sul mercato nuovi contenuti promozionali.

I banner carosello sono contrassegnati da un banner con la parola **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

Nel sito Web, un banner carosello può essere visualizzato come segue:

![chlimage_1-439](assets/chlimage_1-439.png)

Qui è possibile spostarsi tra le immagini (facendo clic sui numeri). Inoltre, le diapositive vengono ruotate automaticamente in base a un intervallo di tempo personalizzabile. Le immagini aggiunte nel banner del carosello supportano sia i punti attivi che le mappe immagine, dove gli utenti possono toccare o passare a un collegamento ipertestuale o accedere a una finestra di visualizzazione rapida.

In questo esempio, un utente ha toccato o fatto clic su una mappa immagine per accedere alla finestra di visualizzazione rapida dei guanti:

![chlimage_1-440](assets/chlimage_1-440.png)

## Scoprite come creare i banner carosello {#watch-how-carousel-banners-are-created}

Seguite la procedura dettagliata di 10 e 33 secondi sulla [creazione](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)dei banner carosello. Inoltre verrà illustrato come visualizzare in anteprima, modificare e distribuire i banner carosello.

>[!NOTE]
>
>Per poter creare o modificare i banner del carosello, gli utenti non amministrativi devono essere aggiunti al gruppo **[!UICONTROL dam-users]** . In caso di problemi durante la creazione o la modifica, rivolgiti all’amministratore di sistema, che può aggiungere utenti al gruppo **[!UICONTROL dam-users ]**.

## Avvio rapido: Banner carosello {#quick-start-carousel-banners}

Per iniziare subito a lavorare:

1. [Identificare le variabili](#identifying-hotspot-and-image-map-variables) dei punti di attivazione e delle mappe immagine (solo per i clienti che utilizzano AEM Assets + Dynamic Media)

   Per iniziare, identificate le variabili dinamiche utilizzate dall’implementazione esistente della visualizzazione rapida in modo da poter inserire correttamente i punti di attivazione e i dati delle mappe immagine durante il processo di creazione dei banner carosello in AEM Assets.

   >[!NOTE]
   >
   >Se siete AEM Sites o clienti di e-commerce, potete utilizzare la funzione integrata per passare alle pagine di prodotto e cercare le interfacce esistenti nel catalogo di prodotti. Non è necessario immettere manualmente le variabili per punti attivi o per mappe immagine. Consultate le informazioni sulla [configurazione di eCommerce](/help/sites-administering/generic.md).
   >
   >
   >Se siete AEM Assets e clienti Dynamic Media, immettete manualmente i dati per i punti di attivazione e le mappe immagine, quindi integrate l’URL pubblicato o il codice da incorporare con il sistema di gestione dei contenuti di terze parti.

1. Facoltativo: se necessario, [crea un predefinito visualizzatore per set carosello](/help/assets/managing-viewer-presets.md).

   Gli amministratori possono personalizzare il comportamento e l’aspetto del carosello creando un proprio predefinito per visualizzatori Carosello. Il vantaggio principale è che potete riutilizzare questo predefinito per visualizzatori personalizzati per più caroselli. Tuttavia, gli utenti possono anche personalizzare direttamente il comportamento e l’aspetto del carosello durante la creazione del carosello. Questo è l’approccio preferito quando si desidera un design molto specifico per un determinato carosello.

1. [Caricate un banner](#uploading-image-banners)immagine.

   Caricate i banner immagine da rendere interattivi.

1. [Create un set](#creating-carousel-sets)carosello.

   In Set caroselli, gli utenti si spostano tra le immagini dei banner e toccano i punti attivi o le mappe immagine per accedere ai contenuti pertinenti.

   Per creare un set carosello all’interno di Assets, tocca **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL Set carosello.]** Aggiungi le risorse alle diapositive e tocca **[!UICONTROL Salva.]** Inoltre, puoi modificare l’aspetto e il comportamento del carosello direttamente nell’editor.

1. [Aggiungete punti di attivazione o mappe immagine a un banner immagine.](#adding-hotspots-or-image-maps-to-an-image-banner)

   Aggiungete uno o più punti di attivazione o mappe immagine a un banner immagine e associateli a un’azione come un collegamento, una visualizzazione rapida o un frammento esperienza. Dopo aver aggiunto punti di attivazione o mappe immagine, potete completare questa attività pubblicando il set di caroselli. Con la pubblicazione viene creato il codice da incorporare da copiare e applicare alla pagina di destinazione del sito Web.

   Consultate [(Facoltativo) Anteprima dei banner](#optional-previewing-carousel-banners) carosello - Opzionale. Se necessario, potete visualizzare una rappresentazione del set carosello e verificarne l’interattività.

1. [Pubblicare Banner Carosello.](#publishing-carousel-banners)

   Potete pubblicare un set di caroselli come qualsiasi altra risorsa. In Risorse, andate al set carosello, selezionatelo e toccate **[!UICONTROL Pubblica.]** Quando si pubblica un set carosello, vengono attivati l’URL e la stringa da incorporare.

1. Effettua una delle operazioni seguenti:

   * [Aggiungere un banner carosello alla pagina del sito Web
      ](#adding-a-carousel-banner-to-your-website-page)Potete aggiungere nella pagina del sito Web l’URL del banner carosello o il codice da incorporare copiato.

      * [Integrare il banner del carosello con una visualizzazione rapida](#integrating-the-carousel-banner-with-an-existing-quickview)esistente. Se utilizzate un sistema di gestione dei contenuti Web di terze parti, dovrete integrare il nuovo banner carosello con l’implementazione esistente di Quickview sul sito Web.
   * [Aggiungere un banner carosello al sito Web in AEM
      ](/help/assets/adding-dynamic-media-assets-to-pages.md)Se siete AEM Sites, potete aggiungere il set carosello direttamente alla pagina in AEM, utilizzando il componente Supporto interattivo.


Per modificare i set di caroselli, consultate [Modifica dei set di caroselli.](#editing-carousel-sets) Inoltre, potete visualizzare e modificare le proprietà [del set](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/managing-assets-touch-ui.html#editing-properties)carosello.

## Identificazione delle variabili dei punti di attivazione e delle mappe immagine {#identifying-hotspot-and-image-map-variables}

Per iniziare, identificate le variabili dinamiche utilizzate dall’implementazione esistente della visualizzazione rapida in modo da poter inserire correttamente i punti di attivazione o i dati delle mappe immagine durante il processo di creazione dei set carosello in AEM Assets.

Quando aggiungete punti di attivazione o mappe immagine a un&#39;immagine del banner in AEM Assets, dovete assegnare un SKU e variabili aggiuntive facoltative a ogni punto di attivazione o mappa immagine. Tali variabili vengono utilizzate in seguito per far corrispondere punti attivi o mappe immagine con contenuto di visualizzazione rapida.

>[!NOTE]
>
>Se siete AEM Sites e/o clienti AEM e-commerce, ignorate questo passaggio. Non è necessario identificare manualmente le variabili dei punti di attivazione o delle mappe immagine; potete utilizzare l&#39;integrazione con Ecommerce per l&#39;integrazione dei prodotti. Consultate le informazioni sulla [configurazione di eCommerce](/help/sites-administering/generic.md). Inoltre, potete utilizzare il componente Interattivo e aggiungerlo alla pagina Web.
>
>Se siete AEM Assets o clienti Media, pubblicate l’URL o il codice da incorporare, quindi integrate con il sistema di gestione dei contenuti di terze parti e identificate manualmente i punti di attivazione e le mappe immagine.

È importante identificare in modo appropriato il numero e il tipo di variabili da associare ai dati dei punti di attivazione o delle mappe immagine. Ogni punto sensibile o mappa immagine aggiunta a un&#39;immagine banner deve contenere informazioni sufficienti per identificare in modo chiaro il prodotto nel sistema di back-end esistente. Allo stesso tempo, ogni punto di attivazione o mappa immagine non deve includere più dati del necessario. Questo perché renderebbe il processo di immissione dei dati eccessivamente complesso e la gestione dei punti attivi o delle mappe immagine più soggetta a errori.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati di aree sensibili o mappe immagine.

A volte può essere sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione della visualizzazione rapida, in quanto è probabile che sappiano qual è il set minimo di dati necessario per identificare la visualizzazione rapida nel sistema. Tuttavia, nella maggior parte dei casi è anche possibile analizzare semplicemente il comportamento esistente del codice front-end.

La maggior parte delle implementazioni di visualizzazione rapida utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, questo accade quando tocca un pulsante **[!UICONTROL Quick View (Visualizzazione rapida)]**.
* Il sito Web invia una richiesta Ajax al back-end per caricare i dati della visualizzazione rapida o il contenuto, se necessario.
* I dati della visualizzazione rapida vengono convertiti nel contenuto in preparazione del rendering sulla pagina Web.
* Infine, il codice front-end esegue visivamente il rendering di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito Web esistente in cui è implementata la funzione di visualizzazione rapida, attivare la visualizzazione rapida e acquisire l’URL Ajax inviato dalla pagina Web per caricare i dati di visualizzazione rapida o il contenuto.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser Web moderni dispongono di ispettori Web che eseguono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser Web che includono ispettori Web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere F12 (Windows) o Comando-Opzione-I (Mac) per aprire il pannello Strumenti per sviluppatori, quindi toccare la scheda Rete.
* In Firefox, è possibile attivare il plug-in Firebug premendo F12 (Windows) o Comando-Opzione-I (Mac) e utilizzare la relativa scheda Net, oppure è possibile utilizzare lo strumento integrato Ispettore e la relativa scheda Rete.

Quando il monitoraggio della rete è attivato nel browser, attiva la visualizzazione rapida sulla pagina.

Ora trova l&#39;URL Ajax della visualizzazione rapida nel registro di rete e copia l&#39;URL registrato per analisi future. Nella maggior parte dei casi, quando si attiva la visualizzazione rapida, vengono inviate al server numerose richieste. In genere, l’URL Ajax della visualizzazione rapida è uno dei primi dell’elenco. Dispone di una porzione o di un percorso di una stringa di query complessa e il tipo MIME della risposta è `text/html`, `text/xml`o `text/javascript`.

Durante questo processo è importante visitare diverse aree del sito Web, con diverse categorie e tipi di prodotti. Il motivo è che gli URL di visualizzazione rapida possono avere parti comuni per una determinata categoria di siti Web, ma possono essere modificati solo se visitate un’area diversa del sito Web.

Nel caso più semplice, l’unica parte variabile nell’URL della visualizzazione rapida è lo SKU del prodotto. In questo caso, il valore SKU è l’unico dato necessario per aggiungere aree sensibili o mappe immagine all’immagine del banner.

Tuttavia, in casi complessi, l’URL di visualizzazione rapida presenta elementi diversi oltre allo SKU, come ID categoria, codice colore, codice dimensione e così via. In questi casi, ogni elemento è una variabile separata nella definizione dei dati del punto di attivazione o della mappa immagine nella funzione del banner del carosello.

Considerate i seguenti esempi di URL di visualizzazione rapida e le relative variabili di aree sensibili o mappe immagine risultanti:

<table>
 <tbody>
  <tr>
   <td>SKU singolo, trovato nella stringa di query.</td>
   <td><p>Gli URL di visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L’unica parte variabile dell’URL è il valore del parametro della stringa di <code>productId=</code> query, che è chiaramente un valore SKU. Pertanto, i nostri punti di attivazione o le nostre mappe immagine richiedono solo campi SKU popolati con valori come <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>SKU singolo, trovato nel percorso dell’URL.</td>
   <td><p>Gli URL di visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU dei punti attivi/mappe immagine:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID categoria nella stringa di query.</td>
   <td><p>Gli URL di visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU è memorizzato nel <code>prodId</code> parametro e l'ID categoria è memorizzato nel <code>category=</code>parametro.</p> <p>Di conseguenza, le definizioni di aree sensibili e mappe immagine sono coppie. ovvero un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
     <li><p>SKU è <strong><code>305466</code></strong> ed <code>categoryId</code> è <code>1100004</code>.</p> </li>
     <li><p>SKU è <strong><code>310181</code></strong> ed <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU è <strong><code>308706</code></strong> ed <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Caricamento dei banner immagine {#uploading-image-banners}

Se avete già caricato le immagini da usare, passate al passaggio successivo, [Creazione di set](#creating-carousel-sets)di caroselli. Le immagini utilizzate nel carosello devono essere caricate dopo che Dynamic Media è stato abilitato.

Per caricare i banner immagine, consultate [Caricamento delle risorse](/help/assets/managing-assets-touch-ui.md).

## Creazione di set carosello {#creating-carousel-sets}

>[!NOTE]
>
>Per creare o modificare i banner del carosello, è necessario aggiungere utenti non amministrativi al gruppo **[!UICONTROL dam-users]** . In caso di problemi durante la creazione o la modifica, rivolgiti all’amministratore di sistema, che può aggiungere utenti al gruppo **[!UICONTROL dam-users]** .

**Per creare un set carosello**

1. In Risorse, individuate la cartella in cui desiderate creare il set carosello e toccate **[!UICONTROL Crea > Set carosello.]**
1. Nella pagina Editor banner carosello toccate **[!UICONTROL Toccate per aprire il selettore]** delle risorse e selezionare l’immagine per la prima diapositiva.

   Nella pagina Editor banner carosello, effettuate una delle seguenti operazioni:

   * Vicino all&#39;angolo superiore sinistro della pagina, toccate l&#39;icona **[!UICONTROL Aggiungi diapositiva]** .

   * Vicino al centro della pagina, toccate **[!UICONTROL Toccate per aprire il selettore delle risorse.]**

   Tocca per selezionare le risorse da includere nel Set carosello. Le risorse selezionate dispongono di un’icona a forma di segno di spunta. Al termine della procedura, vicino all’angolo superiore destro della pagina, tocca **[!UICONTROL Seleziona**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando o facendo clic su **[!UICONTROL Invio.]** Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e tocca l’icona **[!UICONTROL Filtro]** nella barra degli strumenti. Per modificare la visualizzazione, tocca l’icona Visualizza e fai clic su **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a elenco.]**

   Per ulteriori informazioni, consulta [Uso dei selettori](/help/assets/working-with-selectors.md) .

1. Continuate ad aggiungere diapositive finché non avrete aggiunto tutte le immagini da ruotare nel set carosello.
1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Se necessario, trascinate le diapositive per riordinare le immagini nell’elenco del set.
   * Per eliminare un’immagine, selezionatela, quindi toccate **[!UICONTROL Elimina diapositiva]** sulla barra degli strumenti.

   * Per applicare un predefinito, toccate l’elenco a discesa dei predefiniti accanto all’angolo superiore destro della pagina, quindi selezionate un predefinito da applicare al set contemporaneamente.
   Per eliminare una diapositiva, toccate o fate clic sulla diapositiva e toccate o fate clic su **[!UICONTROL Elimina diapositiva]** nella barra degli strumenti. Per spostare una diapositiva, toccate l’icona del reoreder, quindi tenete premuto e spostatevi nella posizione desiderata.

1. Dopo aver aggiunto le immagini nelle diapositive, potete aggiungere un punto di attivazione, una mappa immagine o entrambi all’immagine. Consultate [Aggiunta di aree sensibili o mappe](#adding-hotspots-or-image-maps-to-an-image-banner)immagine.
1. Per modificare la progettazione visiva e il comportamento dei set carosello, toccate o fate clic sulle schede Comportamento e Aspetto e apportate le modifiche necessarie per ottenere l’aspetto del banner carosello o per determinare il funzionamento di componenti specifici. Consultate [Gestione dei predefiniti](/help/assets/viewer-presets.md) per visualizzatori per ulteriori informazioni sull’utilizzo dell’editor per visualizzatori.

   >[!NOTE]
   >
   >Per i banner carosello, potete regolare quanto segue:
   >    * Durata della visualizzazione di un’immagine. Per impostazione predefinita, ogni immagine viene visualizzata per 9 secondi.
   >    * Animazione. Per impostazione predefinita, ogni transizione di diapositiva è una dissolvenza. È possibile modificare questa impostazione in una transizione diapositiva.
   >    * Stile dei pulsanti. Gli utenti possono ruotare i banner toccando ogni punto o numero. È possibile modificare la posizione in cui appaiono i pulsanti degli indicatori di set (e se si tratta di uno stile numerico o punteggiato) e le loro dimensioni.
   >    * Modifica lo stile di evidenziazione di una mappa immagine o dell’icona utilizzata per i punti di attivazione.
   >    * Prima di modificare un predefinito per visualizzatori, scegliete lo stile su cui basare il predefinito. In caso contrario, quando iniziate a modificare il predefinito per visualizzatori, tutte le modifiche apportate andranno perdute se decidete di passare a un altro predefinito

   >
   >
   >Consultate Considerazioni [speciali per i banner](/help/assets/viewer-presets.md#specialconsiderationsforcreatingacarouselbannerviewerpreset) carosello per istruzioni dettagliate e ulteriori informazioni sull’editor visualizzatore.

   Potete anche visualizzare l’anteprima dell’aspetto del banner del carosello. Consultate [(Facoltativo) Anteprima Dei Banner](#optional-previewing-carousel-banners)Carosello.

1. Toccate **[!UICONTROL Salva]** al termine.

## Aggiunta di punti attivi o mappe immagine a un banner immagine {#adding-hotspots-or-image-maps-to-an-image-banner}

Potete aggiungere punti attivi o mappe immagine a un banner utilizzando l&#39;editor di set carosello.

Quando aggiungete aree sensibili o mappe immagine, potete definirle come una visualizzazione a comparsa Quickview, come un collegamento ipertestuale o un frammento esperienza.

Consulta Frammento [](/help/sites-authoring/experience-fragments.md)esperienza.

>[!NOTE]
>
>Gli strumenti di condivisione social media in Carosello Banner non sono supportati quando incorporate il visualizzatore in un frammento esperienza.
Per ovviare a questo problema, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.

Quando aggiungete punti di attivazione o mappe immagine a un’immagine, ricordate di salvare il lavoro. Le opzioni Annulla e Ripristina, accanto all’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione del banner carosello, potete facoltativamente utilizzare Anteprima per visualizzare una rappresentazione dell’aspetto del banner carosello per i clienti.

Consultate [(Facoltativo) Anteprima Dei Banner Carosello.](#optional-previewing-carousel-banners)

>[!NOTE]
>
>Quando aggiungete punti di attivazione a un’immagine in un’immagine [](/help/assets/interactive-images.md) interattiva o in un banner carosello, le informazioni relative ai punti di attivazione vengono memorizzate nella stessa posizione dei metadati, in relazione alla posizione e alla modalità dell’immagine, indipendentemente dal fatto che si tratti di un’immagine interattiva o di un banner carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai dati dei punti di attivazione definiti, in entrambi i visualizzatori.

>Tenete presente, tuttavia, che i banner carosello supportano le mappe immagine sulle immagini che possono anche contenere punti di attivazione; un’immagine interattiva non lo è. Tenete presente questo aspetto se intendete creare un&#39;immagine interattiva o un banner carosello che utilizza la stessa immagine. È possibile creare immagini interattive e banner carosello utilizzando copie separate della stessa immagine.

>[!NOTE]
Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono rimossi.

Consulta anche [Aggiunta di mappe immagine](/help/assets/image-maps.md).

**Per aggiungere punti attivi o mappe immagine a un banner immagine**

1. Da Risorse, andate al set di caroselli da rendere interattivo.
1. Selezionate il set carosello e toccate **[!UICONTROL Modifica.]** Viene aperto l’Editor visualizzatore carosello.
1. Selezionate la diapositiva da rendere interattiva.
1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Punto attivo]** o **[!UICONTROL Mappa immagine.]**
1. Effettuate una delle seguenti operazioni:

   * Per i punti attivi: Sull&#39;immagine, toccate la posizione in cui desiderate visualizzare il punto di attivazione.
   * Per le mappe immagine: Sull’immagine, fate clic, quindi trascinate dall’alto a sinistra verso il basso a destra per creare l’area della mappa immagine. Per regolare le dimensioni della mappa immagine, trascinatene gli angoli.

   Se necessario, trascinate il punto di attivazione o la mappa immagine in una nuova posizione. Se necessario, potete aggiungere altri punti di attivazione o mappe immagine.

   Per eliminare un punto attivo o una mappa immagine, tocca la scheda **[!UICONTROL Azioni]**. Seleziona il nome del punto attivo o della mappa immagine da rimuovere dall’intestazione **[!UICONTROL Mappe e punti attivi]** del menu a discesa **[!UICONTROL Tipo selezionato]**. Tocca l’icona **[!UICONTROL Cestino]** accanto al menu, quindi seleziona **[!UICONTROL Elimina.]**

1. Nel campo di testo Nome, digitate il nome del punto di attivazione o della mappa immagine. Questo nome viene visualizzato anche nell&#39;elenco a discesa **[!UICONTROL Mappe e punti di attivazione]** . Fornendo un nome è facile identificare il punto di attivazione o la mappa immagine se si decide di apportare modifiche in futuro.
1. Nella scheda **[!UICONTROL Azioni]** , effettuare una delle seguenti operazioni:

   * Toccate **[!UICONTROL Visualizzazione rapida.]**

      * Se siete AEM Sites e clienti e-commerce, toccate l&#39;icona del selettore prodotto (lente di ingrandimento) per aprire la pagina Selezione prodotto. Toccate il prodotto che desiderate utilizzare, quindi toccate il segno di spunta nell’angolo superiore destro della pagina per tornare all’Editor carosello banner.
      * Se non siete un cliente AEM Sites o di e-commerce

         * Consultate [Identificazione delle variabili](#identifying-hotspot-and-image-map-variables) dei punti di attivazione in base alle vostre esigenze.
         * Quindi, immettete manualmente il valore SKU. Nel campo di testo Valore SKU, digitare lo SKU del prodotto (Stock Keeping Unit), che è un identificatore univoco per ogni prodotto o servizio distinto offerto. Il valore SKU immesso popola automaticamente la porzione variabile del modello di visualizzazione rapida in modo che il sistema sappia associare il punto di attivazione toccato a una particolare visualizzazione rapida dello SKU.
         * (Facoltativo) Se nella visualizzazione rapida sono presenti altre variabili che è necessario utilizzare per identificare ulteriormente un prodotto, toccate **[!UICONTROL Aggiungi variabile generica.]** Nel campo di testo, specificate una variabile aggiuntiva. Ad esempio, category=Mens è una variabile aggiunta.

         * Per ulteriori informazioni, consulta [Uso dei selettori](/help/assets/working-with-selectors.md) .
   * Toccate **[!UICONTROL Collegamento ipertestuale.]**

      * Se siete AEM Sites, toccate l&#39;icona Selettore sito (cartella) per passare a un URL.
         >[!NOTE]
         Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con collegamenti alle pagine di AEM Sites.

      * Se siete clienti indipendenti, nel campo HREF specificate il percorso completo dell’URL di una pagina Web collegata.

   Accertatevi di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Per ulteriori informazioni, consulta [Uso dei selettori](/help/assets/working-with-selectors.md) .

   * Tap **[!UICONTROL Experience Fragment.]**

      * Se siete un cliente AEM Sites, toccate l’icona di ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza. Toccate o fate clic sul frammento esperienza che desiderate utilizzare, quindi toccate Seleziona nell&#39;angolo superiore destro della pagina per tornare alla pagina di gestione dell&#39;area sensibile.
Consulta Frammenti [](/help/sites-authoring/experience-fragments.md)esperienza.

      * Specificate la larghezza e l&#39;altezza del frammento esperienza così come apparirà sul banner.

         >[!NOTE]
         Gli strumenti di condivisione social media in Carosello Banner non sono supportati quando incorporate il visualizzatore in un frammento esperienza.
Per ovviare a questo problema, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   Potete anche visualizzare l’anteprima dell’aspetto del banner del carosello. Consultate [(Facoltativo) Anteprima Dei Banner](#optional-previewing-carousel-banners)Carosello.

1. Toccate **[!UICONTROL Salva.]**
1. Pubblicate il set carosello. La pubblicazione crea il codice da incorporare o l’URL che potete utilizzare nella pagina del sito Web. Se siete AEM Sites, potete aggiungere il set carosello direttamente alla pagina Web.

   Consultate [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md).

   Consultate [Aggiunta di un set carosello alla pagina di destinazione del sito Web](#adding-a-carousel-banner-to-your-website-page)

## Modifica dei set di caroselli {#editing-carousel-sets}

>[!NOTE]
Per poter creare o modificare i banner del carosello, gli utenti non amministrativi devono essere aggiunti al gruppo **[!UICONTROL dam-users]** . In caso di problemi durante la creazione o la modifica, rivolgiti all’amministratore di sistema, che può aggiungere utenti al gruppo **[!UICONTROL dam-users]** .

Potete eseguire diverse attività di modifica su Set carosello, ad esempio:

* Aggiungete le diapositive a un set carosello. Consultate anche [Utilizzo dei selettori](/help/assets/working-with-selectors.md).
* Riordinare le diapositive nel set carosello.
* Eliminate le risorse nel set carosello.
* Applicate un predefinito per visualizzatori.
* Eliminate il set di caroselli.
* Aggiungere o modificare punti di attivazione e mappe immagine. Consultate anche [Utilizzo dei selettori](/help/assets/working-with-selectors.md).

**Per modificare un set di caroselli**

1. Effettuate una delle seguenti operazioni:

   * Passate il puntatore del mouse su una risorsa Set carosello, quindi toccate **[!UICONTROL Modifica]** (icona matita).
   * Passate il puntatore del mouse su una risorsa Set carosello, toccate **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi toccate **[!UICONTROL Modifica]** sulla barra degli strumenti.

   * Tap on a Carousel Set asset, then in the upper-left corner of the page tap **[!UICONTROL Edit]** (pencil icon).

1. Per modificare il set di caroselli, effettuate una delle seguenti operazioni:

   * To add a slide, tap the **[!UICONTROL Add Slide]** icon then navigate to the asset you want to add to that slide and tap or click the checkmark.
   * Per riordinare le diapositive, trascinate una diapositiva in una nuova posizione (selezionate l’icona di riordinamento per spostare gli elementi).
   * Per aggiungere un punto di attivazione o una mappa immagine, fate clic sulle icone del punto di attivazione o della mappa immagine e consultate [Aggiunta di punti di attivazione e mappe](#adding-hotspots-or-image-maps-to-an-image-banner)immagine.
   * To edit the appearance or behavior of the carousel set, tap the **[!UICONTROL Appearance]** tab or **[!UICONTROL Behavior]** tab, then set the options you want.
   * Per modificare punti di attivazione o mappe immagine, nella diapositiva appropriata selezionate un punto di attivazione o una mappa immagine e apportate le modifiche necessarie nella scheda **[!UICONTROL Azioni]** .
   * Per eliminare una diapositiva, selezionatela, quindi toccate **[!UICONTROL Elimina diapositiva]** sulla barra degli strumenti.
   * To apply a preset, near the upper-right corner of the page, tap the **[!UICONTROL Preset]** drop-down list, then select a viewer preset.
   * Per eliminare un intero set carosello, portatevi sul set carosello, selezionatelo, quindi toccate **[!UICONTROL Elimina.]**

   >[!NOTE]
   Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono rimossi.

## (Facoltativo) Anteprima dei banner carosello {#optional-previewing-carousel-banners}

Potete utilizzare Anteprima per vedere l’aspetto del banner carosello per i clienti e per testare i punti di attivazione e le mappe immagine dei banner del carosello per assicurarvi che si comportino come previsto.

Una volta ottenuto il risultato desiderato, potete pubblicarlo.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/embed-code.md).
See [Linking URLs to your web application](/help/assets/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con collegamenti alle pagine di AEM Sites.
See [Adding Dynamic Media Assets to pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Potete visualizzare in anteprima i banner del carosello dall’Editor carosello (metodo preferito) o dall’elenco **[!UICONTROL Visualizzatori]** .

**Per visualizzare in anteprima i banner del carosello**

1. In **[!UICONTROL Risorse]**, andate a un banner carosello esistente creato e toccate per aprirlo.
1. Toccate **[!UICONTROL Modifica.]**
1. Nell’elenco dei predefiniti per visualizzatori nell’angolo a destra della barra degli strumenti, selezionate un visualizzatore per l’anteprima del banner carosello.

   ![experience_fragment-carouselbanner-viewermenu a discesa](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Toccate **Anteprima.]**
1. Toccate i punti di attivazione o le mappe immagine sull’immagine per verificare le azioni associate.

**Per visualizzare in anteprima i banner del carosello dall&#39;elenco Visualizzatori**

1. In **[!UICONTROL Risorse]**, andate a un banner carosello esistente creato e toccate per aprirlo.
1. Nell’angolo in alto a sinistra della pagina Anteprima, fate clic sull’icona Contenuto.
1. Nell’elenco **[!UICONTROL Visualizzatori]** nel pannello sul lato sinistro della pagina, toccate il nome del predefinito per visualizzatori di banner carosello da usare.
1. Toccate i punti di attivazione o le mappe immagine sull’immagine per verificare le azioni associate.

## Pubblicazione dei banner carosello {#publishing-carousel-banners}

Per utilizzarlo, è necessario pubblicare il carosello. Quando si pubblica un set carosello, vengono attivati l’URL e il codice da incorporare. Il carosello viene anche pubblicato su Dynamic Media cloud, integrato con un CDN per la distribuzione scalabile e performante.

>[!NOTE]
Se utilizzate un&#39;immagine interattiva esistente con punti di attivazione per il banner del carosello, dopo aver pubblicato il banner del carosello dovete pubblicare separatamente l&#39;immagine interattiva.
Inoltre, se modificate un&#39;immagine interattiva già pubblicata che state utilizzando in un banner carosello, è necessario pubblicare l&#39;immagine interattiva prima che tali modifiche si riflettano nel banner del carosello.

Consultate [Pubblicazione di risorse](/help/assets/publishing-dynamicmedia-assets.md) Dynamic Media per informazioni su come pubblicare i banner del carosello.

## Aggiunta di un banner carosello alla pagina del sito Web {#adding-a-carousel-banner-to-your-website-page}

Dopo aver caricato le immagini dei banner per creare un carosello, aggiunto punti di attivazione e/o mappe immagine al banner e pubblicato il set di caroselli, potete ora aggiungerlo alla pagina del sito Web esistente.

>[!NOTE]
Se siete AEM Sites, potete aggiungere il banner del carosello direttamente alla pagina trascinando il componente Supporto interattivo sulla pagina. See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Tuttavia, se siete clienti indipendenti di Risorse AEM, potete aggiungere manualmente il banner carosello alla pagina di destinazione del sito Web, come descritto in questa sezione.

1. Copiate il codice da incorporare del set carosello pubblicato.
See [Embedding the Video or Image Viewer on a Web Page](/help/assets/embed-code.md).

1. Aggiungete il codice da incorporare copiato dai AEM Assets alla pagina Web.
Il codice da incorporare copiato è reattivo e dovrebbe quindi adattarsi automaticamente all&#39;area di incorporamento della pagina.

## Integrazione del banner carosello con una visualizzazione rapida esistente {#integrating-the-carousel-banner-with-an-existing-quickview}

Nota: questo passaggio si applica solo se sei un cliente AEM Assets standalone.

L’ultimo passaggio di questo processo consiste nell’integrare il banner del carosello con un’implementazione esistente della visualizzazione rapida sul sito Web. Ogni implementazione rapida della visualizzazione è unica ed è necessario un approccio specifico che molto probabilmente coinvolga l&#39;assistenza di una persona IT front-end.

L’implementazione della visualizzazione rapida esistente rappresenta in genere una catena di azioni correlate che si verificano sulla pagina Web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito Web.
1. Il codice front-end ottiene un URL di visualizzazione rapida basato sull’elemento dell’interfaccia utente attivato al punto 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto al punto 2.
1. La logica di backend restituisce i dati di visualizzazione rapida corrispondenti o il contenuto al codice front-end.
1. Il codice front-end carica i dati o il contenuto della visualizzazione rapida.
1. Facoltativamente, il codice front-end converte i dati della visualizzazione rapida caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l&#39;utente finale.

Queste chiamate potrebbero non rappresentare chiamate API pubbliche indipendenti che possono essere richiamate dalla logica della pagina Web da un passaggio arbitrario. Si tratta, invece, di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Contemporaneamente alla sostituzione del passaggio 1 e in parte del passaggio 2 da parte del banner carosello, quando un utente fa clic su un punto di attivazione o una mappa immagine all’interno del banner carosello, tale interazione viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina Web che contiene tutti i dati di aree sensibili o mappe immagine precedentemente aggiunti.

In un tale gestore di eventi, il codice front-end esegue le seguenti operazioni:

* Ascolta un evento emesso dal banner del carosello.
* Crea un URL di visualizzazione rapida basato sui dati del punto di attivazione o della mappa immagine.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering sullo schermo per la visualizzazione.

Il codice da incorporare restituito dai AEM Assets ha già un gestore eventi ready-to-use in posizione commentata.

Pertanto, è solo necessario rimuovere il commento dal codice e sostituire il corpo fittizio del gestore con il codice specifico per la pagina Web specifica.

Il processo di creazione dell’URL di visualizzazione rapida è sostanzialmente opposto a quello utilizzato per identificare le variabili dei punti di attivazione e delle mappe immagine trattate in precedenza.

Consultate [Identificazione delle variabili](#identifying-hotspot-and-image-map-variables)dei punti di attivazione e delle mappe immagine.

L’ultimo passaggio per attivare l’URL della visualizzazione rapida e attivare il pannello di visualizzazione rapida richiede probabilmente l’assistenza di un addetto IT front-end del reparto IT. Essi hanno la capacità di sapere come attivare con precisione l’implementazione della visualizzazione rapida dal passaggio corretto, con un URL di visualizzazione rapida pronto all’uso.

## Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/custom-pop-ups.md).
