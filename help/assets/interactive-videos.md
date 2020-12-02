---
title: Video interattivi
description: Scopri come lavorare con video interattivi e video acquistabili in Dynamic Media
uuid: c3ff6839-fff5-4709-8163-5c4245b80e6d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 04be55f2-c7d8-45ef-89e5-58856b971de5
docset: aem65
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '6056'
ht-degree: 5%

---


# Video interattivi{#interactive-videos}

Potete creare facilmente dei video interattivi, noti anche come video acquistabili, che guidano la conversione direttamente dal video. Il coinvolgimento dei clienti con il video si svolge in un pannello accanto al lettore video, dove vengono visualizzate le relative miniature di servizi, informazioni o prodotti in base alle funzioni presenti nel video. I clienti possono toccare la miniatura ed essere collegati direttamente al servizio oppure aggiungere l&#39;elemento a un carrello per un acquisto immediato, oppure essere collegati a una pagina Web per ulteriori informazioni.

Al termine del video, viene visualizzato un riepilogo visivo di tutte le offerte per avviare una chiamata all&#39;azione. I clienti hanno un&#39;altra opportunità di toccare l&#39;elemento desiderato. Esperienze fruibili e specifiche come queste aumentano il coinvolgimento e la conversione dei clienti.

Vedere anche [Immagini interattive](/help/assets/interactive-images.md).

## Video interattivo in azione {#interactive-video-in-action}

Per visualizzare un video interattivo e commerciabile in azione, fate clic su [Live Demos](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html), scorrete fino al titolo **[!UICONTROL Shoppable Media]** nella pagina, quindi fate clic sul video shoppable.

* Durante la riproduzione, quando i prodotti vengono utilizzati nel video, il prodotto identico appare a destra come una miniatura.

* Fate clic sulla miniatura per mettere in pausa il video e aprire la visualizzazione rapida del prodotto. Ad esempio, fate clic sulla miniatura di KitchenAid nel video per vedere la rotazione a 360 gradi del mixer oppure ingrandite per visualizzare i dettagli del mixer.

<!-- There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![Fotogramma da un ](assets/chlimage_1-126.png) *video interattivo acquistabileAcquisizione di un fotogramma video da un video interattivo acquistabile.*

>[!NOTE]
>
>Se create un video interattivo per avviare una pagina Web quando un utente fa clic su una miniatura, alcuni dispositivi impediranno l’apertura della pagina Web a comparsa. In tali casi, è necessario modificare l&#39;impostazione del blocco dei pop-up sul dispositivo. Ad esempio, su un iPhone 6 Apple, toccate **[!UICONTROL Settings]** > **Safari** > **Blocca finestre a comparsa**, quindi fate scorrere il controllo su **[!UICONTROL Disattivato]**. Ora, quando riproducete un video interattivo e fate clic su una miniatura, viene richiesto se desiderate aprire la finestra a comparsa. Se accettate, viene visualizzata la pagina Web.

### Guarda come vengono creati i video interattivi {#watch-how-interactive-videos-are-created}

Segui la procedura dettagliata della durata di 7 minuti e 30, durante la quale [avviene la creazione dei video interattivi](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo) [](https://outv.omniture.com?v=s4NHQ2dzqd7hIqWjeG2sIdyNWsTWyupA).
Anche se la procedura dettagliata per i video è contrassegnata con la dicitura Assets on Demand, i principi e i passaggi illustrati restano validi per i video interattivi di AEM Assets.

### Webinar  successo cliente Adobe {#adobe-customer-success-webinar}

Il webinar &quot;Using Interactive Video, Link Sharing, and YouTube sharing in  AEM Assets&quot; (Utilizzo di video interattivi, condivisione di collegamenti e condivisione di YouTube in) spiega come usare video interattivi e altre funzioni per collegare gli eventi basati sulla conversione ai contenuti di marketing dei video.

>[!NOTE]
[Utilizzo di video interattivi, condivisione di collegamenti e condivisione di YouTube in  AEM Assets](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/).

## Avvio rapido: Video interattivi {#quick-start-interactive-videos}

La seguente descrizione dettagliata del flusso di lavoro è stata creata per consentirvi di imparare a usare rapidamente i video interattivi in Contenuti multimediali dinamici.

Cercare l&#39;intestazione **Esempio** all&#39;interno di alcune delle attività di Avvio rapido. Contiene una breve esercitazione basata su questa pagina Web della demo iniziale che *non* contiene ancora interattività:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

Gli **esempi** illustrano i passaggi necessari per integrare i video interattivi nel sito web.

Al termine dell&#39;esercitazione nell&#39;ultima sezione Esempio, la pagina Web della demo finale con il video interattivo completamente integrato avrà il seguente aspetto:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

Passaggi video interattivi:

1. **(Facoltativo) Identificazione delle variabili**  Quickview - Iniziate identificando le variabili dinamiche utilizzate dall’implementazione esistente di Quickview. Le variabili vengono utilizzate per mappare le miniature dei prodotti sulla visualizzazione rapida del prodotto corrispondente al momento della creazione del video interattivo. Vedere [(facoltativo) Identificazione delle variabili di visualizzazione rapida](#optional-identifying-quickview-variables).
   *Questo passaggio è obbligatorio solo se tutte le informazioni seguenti sono vere*: ・ Per aggiungere interattività al video, attivate la visualizzazione rapida.
・ L&#39;implementazione di AEM non utilizza *un* framework di integrazione di eCommerce per estrarre i dati di prodotto in AEM da qualsiasi soluzione di eCommerce come IBM Websfera Commerce, Elastic Path, hybris o Intershop. Vedere [Concetti di eCommerce in  AEM Assets](/help/sites-administering/concepts.md).

1. **(Facoltativo) Creazione di un predefinito**  per visualizzatori video interattivi - Personalizzate l’aspetto e il comportamento di vari componenti che compongono il lettore, ad esempio la barra di scorrimento video e le miniature interattive.
La creazione di un predefinito per visualizzatori video interattivi non è necessaria se intendete utilizzare i predefiniti per visualizzatori video interattivi forniti con il prodotto `Shoppable_Video_Light` o `Shoppable_Video_Dark`.
Consultate [Creazione di un nuovo predefinito per visualizzatori](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) (facoltativo) e [Considerazioni speciali per la creazione di un predefinito per visualizzatori interattivi](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset).

1. **Caricamento di un video e delle relative risorse**  immagine associate - Caricamento di un video e delle immagini associate da rendere interattive.
Consultate [Caricamento di un video e delle relative risorse di miniature associate](#uploading-a-video-and-its-associated-thumbnail-assets).

1. **Aggiunta di interattività al video** : aggiungete uno o più segmenti di tempo al video. Quindi, associate le miniature delle immagini all’interno di tali segmenti di tempo. Assegnate ciascuna miniatura immagine a un’azione come un collegamento ipertestuale, una visualizzazione rapida o un frammento esperienza.
Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.
Per terminare, pubblicate le risorse video interattive. Con la pubblicazione viene creato il codice o l&#39;URL da copiare e applicare alla pagina di destinazione del sito Web.Vedere [Aggiunta di interattività al video](#adding-interactivity-to-your-video).
Consultate [Pubblicazione di risorse](/help/assets/publishing-dynamicmedia-assets.md).

1. **Aggiunta di un video interattivo al sito Web o al sito Web in**
AEMIse utilizzate  AEM Sites, AEM eCommerce o entrambi, potete aggiungere il video interattivo direttamente a una pagina Web in AEM trascinando il componente Supporto interattivo sulla pagina. Consultate [Aggiunta di risorse multimediali dinamiche alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)
Usate il codice o l’URL da incorporare per integrare il video interattivo con le esperienze del sito Web. Consultate [Integrazione di un video interattivo con il sito Web](#integrating-an-interactive-video-with-your-website).
Se utilizzate un WCM di terze parti (Web Content Manager), dovete integrare il nuovo video interattivo con l’implementazione esistente di Quickview utilizzata sul vostro sito Web. Consultate [Integrazione di un video interattivo con una visualizzazione rapida esistente](#integrating-an-interactive-video-with-an-existing-quickview).
   [Aggiunta di Risorse multimediali dinamiche alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md)

## (Facoltativo) Identificazione delle variabili Quickview {#optional-identifying-quickview-variables}

>[!NOTE]
Questa attività è necessaria solo se sono soddisfatte le seguenti condizioni:
* Per aggiungere interattività al video, attivate l’opzione Visualizzazione rapida.
* L&#39;implementazione di AEM non utilizza *un* framework di integrazione eCommerce per estrarre i dati di prodotto in AEM da qualsiasi soluzione di eCommerce come IBM Webferfera Commerce, Elastic Path, hybris o Intershop. Vedere [Concetti di eCommerce in  AEM Assets](/help/sites-administering/concepts.md).

Se l&#39;implementazione di AEM utilizza eCommerce, puoi saltare questa attività e passare all&#39;attività successiva.

Per iniziare, identificate le variabili dinamiche utilizzate dall’implementazione esistente di Quickview in modo da mappare le miniature dei prodotti sul prodotto corrispondente Quickview durante il processo di creazione di video interattivi.

Quando aggiungete segmenti di tempo a un video, assegnate uno SKU ed eventuali variabili aggiuntive a ciascuna miniatura che aggiungete a un segmento. Tali variabili vengono utilizzate successivamente per visualizzare il prodotto Quickview corretto.

È importante identificare correttamente le variabili necessarie per attivare in modo univoco una visualizzazione rapida del prodotto.

A volte può essere sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione di QuickView esistente. È probabile che conoscano il set minimo di dati necessario per identificare Quickview nel sistema. Tuttavia, nella maggior parte dei casi è anche possibile analizzare semplicemente il comportamento esistente del codice front-end.

La maggior parte delle implementazioni di Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, facendo clic su un pulsante &quot;Quickview&quot;.
* Il sito Web invia una richiesta Ajax al back-end per caricare i dati o il contenuto della visualizzazione rapida, se necessario.
* I dati della visualizzazione rapida vengono convertiti nel contenuto in preparazione del rendering sulla pagina Web.
* Infine, il codice front-end esegue visivamente il rendering di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito Web in cui è implementata la visualizzazione rapida, attivare la visualizzazione rapida e acquisire l’URL Ajax inviato dalla pagina Web per caricare i dati o il contenuto della visualizzazione rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser Web moderni dispongono di ispettori Web che eseguono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser Web che includono ispettori Web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere **F12** (Windows) o **Comando+Opzioni+I** (Mac) per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda **Rete**.

* In Firefox, è possibile attivare il plug-in Firebug premendo **F12** (Windows) o **Comando+Opzione+I** (Mac) e utilizzare la relativa scheda **`[Net]`** oppure è possibile utilizzare lo strumento Ispettore incorporato e la relativa scheda Rete.

* In Internet Explorer attivare lo strumento debugger premendo **F12**.

Quando il monitoraggio della rete è attivato nel browser, attivare la visualizzazione rapida sulla pagina.

Ora trova l’URL Ajax di Quickview nel registro di rete e copia l’URL registrato per l’analisi futura. Nella maggior parte dei casi, quando si attiva la visualizzazione rapida, vengono inviate al server numerose richieste. In genere, l’URL Ajax della visualizzazione rapida è uno dei primi nell’elenco. Dispone di una porzione o di un percorso di una stringa di query complessa e il tipo MIME della risposta è `text/html`, `text/xml` o `text/javascript`.

Durante questo processo è importante visitare diverse aree del sito Web, con diverse categorie e tipi di prodotti. Il motivo è che gli URL di visualizzazione rapida possono avere parti comuni per una determinata categoria di sito Web, ma possono essere modificati solo se visitate un’area diversa del sito Web.

Nel caso più semplice, l’unica parte variabile dell’URL di visualizzazione rapida è lo SKU del prodotto. In questo caso, il valore SKU del prodotto è l’unico dato necessario per aggiungere miniature a un segmento di tempo nel video interattivo in AEM.

Tuttavia, in casi complessi, l’URL Quickview presenta elementi diversi oltre allo SKU del prodotto, come ID categoria, codice colore e così via. In tali casi, ogni elemento di questo tipo diventa una variabile separata nella definizione dei dati delle miniature in AEM.

Considerate i seguenti esempi di URL di visualizzazione rapida e le relative variabili di miniatura:

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
    </ul> <p>L'unica parte variabile dell'URL è il valore del parametro della stringa di query <code>productId=</code>, che è chiaramente un valore SKU. Pertanto, le miniature devono essere compilate solo con campi SKU contenenti valori quali <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU singolo, trovato nel percorso dell’URL.</p> </td>
    <td><p>Gli URL della visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU AEM miniature: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa di query.</p> </td>
    <td><p>Gli URL della visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU è memorizzato nel parametro <code>prodId</code> e l'ID categoria è memorizzato nel parametro <code>category=</code>.</p> <p>Di conseguenza, le definizioni delle miniature sono coppie. ovvero un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
      <li>SKU è <code>305466</code> e <code>categoryId</code> è <code>1100004</code></li>
      <li>SKU è <code>310181</code> e <code>categoryId</code> è <code>1100004</code></li>
      <li>SKU è <code>308706</code> e <code>categoryId</code> è <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Esempio**

Quando l&#39;approccio di cui sopra è applicato al nostro sito Web Esempio, abbiamo una pagina Web con una serie di miniature di prodotto, ognuna con un pulsante &quot;SEE MORE&quot;:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

Dopo aver attivato tutte le Visualizzazioni rapide del prodotto disponibili sulla pagina, viene visualizzato il seguente elenco di richieste Quickview effettuate sul back-end:

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

Osservando queste chiamate al server, le informazioni specifiche per il prodotto sono presenti solo nel percorso della richiesta. Si noti inoltre che la stringa di query non viene utilizzata e che sono coinvolti due tipi distinti di dati:

* Il primo tipo è candele, cuscini, mobili e oggetti di vetro. Puoi chiamare questa &quot;categoria di prodotti&quot;.
* Il secondo tipo è il codice del prodotto, ad esempio 233916597. È possibile supporre che si tratti di &quot;product SKU&quot;.

Considerate queste informazioni, l’intero URL di Quickview presenta il seguente pattern:

`/datafeed/$categoryId$-$SKU$.json`

In base a tale analisi, si conclude che per le miniature è possibile usare le due variabili seguenti: `categoryId` e `SKU`.

Ora potete caricare un video e le relative risorse di miniature.

## (Facoltativo) Creazione di un predefinito per visualizzatori video interattivi {#optional-creating-an-interactive-video-viewer-preset}

Potete saltare questa attività e continuare a eseguire la procedura successiva se intendete utilizzare uno dei tipi predefiniti per visualizzatori video interattivi predefiniti forniti con il prodotto `Shoppable_Video_dark` o `Shoppable_Video_light`.

Quando si fa clic su una miniatura nell’ambiente di authoring viene visualizzata un’anteprima della finestra di dialogo Visualizzazione rapida.

![chlimage_1-21](assets/chlimage_1-127.png)

Facoltativamente, potete creare un predefinito personalizzato per visualizzatori video interattivi. Potete determinare, tra l’altro, lo stile del lettore video, le miniature interattive e la visualizzazione griglia delle miniature che viene visualizzata alla fine del video.

Un predefinito per visualizzatori video interattivi esegue correttamente il rendering del video e di tutti i segmenti della timeline aggiunti. Utilizza anche una visualizzazione rapida predefinita di esempio quando fai clic sulla miniatura di un prodotto in modalità Anteprima per verificarne l’interattività prima della pubblicazione.

Dopo aver salvato il predefinito visualizzatore, lo stato relativo viene impostato automaticamente su **On **nella pagina Predefiniti visualizzatore. Lo stato indica che è visibile nel componente Dynamic Media e ogni volta che lo si utilizza per visualizzare l’anteprima di un video. Accertati anche di pubblicare manualmente il nuovo predefinito visualizzatore.

Consultate [Creazione di un nuovo predefinito per visualizzatori](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) per creare un predefinito per visualizzatori video interattivi personalizzato.

## Caricamento di un video e delle relative risorse di miniature associate {#uploading-a-video-and-its-associated-thumbnail-assets}

Se avete già caricato il video e le risorse delle miniature, passate a [Aggiunta di interattività al video](#adding-interactivity-to-your-video).

Se avete caricato i video o le immagini errati o desiderate eliminare i video o le immagini caricati e non più necessari, consultate [Eliminazione delle risorse](/help/assets/manage-assets.md#deleting-assets).

Per caricare un video e le relative risorse di miniatura:

1. Caricate il video e le relative risorse di miniature nella cartella o nelle cartelle desiderate.

   Consultate [Caricamento delle risorse](/help/assets/manage-assets.md).
Consultate [Caricamento delle risorse tramite la pianificazione dei processi FTP](/help/assets/manage-assets.md).

   Ora aggiungete interattività al video.

## Aggiunta di interattività al video {#adding-interactivity-to-your-video}

Per aggiungere segmenti della timeline a un video, usate l’editor visivo diretto nella pagina Crea video interattivo.

Dopo aver aggiunto i segmenti della timeline, potete aggiungere delle miniature all’interno di ciascun segmento. Per ogni miniatura aggiunta, viene applicata un’azione. Ad esempio, potete applicare una visualizzazione rapida alla miniatura, oppure assegnare un collegamento ipertestuale ad essa o un frammento esperienza.

Vedere [Frammenti esperienza](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
Gli strumenti di condivisione social media in Video interattivo non sono supportati quando incorporate il visualizzatore in un frammento esperienza. Per ovviare a questo problema, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.

>[!NOTE]
Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.

Le opzioni Annulla e Ripristina, accanto all’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Dopo aver salvato il video interattivo, il video viene immediatamente aperto in Anteprima. Da qui potete selezionare un predefinito per visualizzatori video interattivi e riprodurre il video per vedere una rappresentazione approssimativa di come apparirà ai clienti.

Per aggiungere interattività al video:

1. Nella vista Risorse, individuate il video caricato e che desiderate rendere interattivo.
1. Effettua una delle operazioni seguenti:

   * Passate il puntatore del mouse sull&#39;immagine, quindi toccate **[!UICONTROL Seleziona]** (icona a forma di segno di spunta). Sulla barra degli strumenti, toccare **[!UICONTROL Modifica.]**

   * Passa il puntatore del mouse sull&#39;immagine, quindi tocca **[!UICONTROL Altre azioni]** (icona a tre punti) **[!UICONTROL > Modifica.]**

   * Toccate l’immagine per aprirla nella pagina Visualizzazione dettagli. Sulla barra degli strumenti, toccare **[!UICONTROL Modifica.]**

1. Nella pagina Crea video interattivo, effettuate una delle seguenti operazioni:

   * Toccate il pulsante **[!UICONTROL Riproduci]** per avviare la riproduzione del video. Quando un particolare prodotto, servizio o dettaglio da evidenziare viene visualizzato, toccate **[!UICONTROL Aggiungi segmento]** sulla barra degli strumenti. Ripetere l&#39;operazione fino a raggiungere la fine del video.

      Per ogni segmento di tempo aggiunto, potete assegnare una o più miniature e quindi collegare tali miniature alle pagine di prodotto Quickview per consentire ai clienti di acquistare o alle pagine Web per ulteriori informazioni.

   * Toccate il pulsante **[!UICONTROL Riproduci]** per avviare la riproduzione del video. Quando un particolare prodotto, servizio o dettaglio che si desidera evidenziare viene visualizzato, toccare **[!UICONTROL Pausa.]** Toccate  **[!UICONTROL Aggiungi segmento.]**

      Continuate a riprodurre e mettere in pausa il video nei punti lungo la timeline in cui desiderate aggiungere un segmento fino alla fine del video.

1. (Facoltativo) La barra sul **[!UICONTROL Cursore scala timeline]** può essere trascinata a sinistra per ingrandire o a destra per ridurre, permettendoti così di controllare il livello di dettagli che vengono visualizzati nei segmenti aggiunti.

   ![chlimage_1-22](assets/chlimage_1-128.png)

   A seconda della lunghezza del video, per impostazione predefinita la durata del segmento è impostata sui seguenti valori:

   <table>
      <tbody>
        <tr>
        <td><strong>Se la lunghezza del video è...</strong></td>
        <td><strong>Per impostazione predefinita, Durata segmento è impostata su...</strong></td>
        </tr>
        <tr>
        <td>3 minuti o più</td>
        <td>60 secondi</td>
        </tr>
        <tr>
        <td>2-3 minuti</td>
        <td>30 secondi</td>
        </tr>
        <tr>
        <td>1-2 minuti</td>
        <td>20 secondi<br /> </td>
        </tr>
        <tr>
        <td>30-60 secondi</td>
        <td>10 secondi</td>
        </tr>
        <tr>
        <td>30 secondi o meno</td>
        <td>5 secondi</td>
        </tr>
      </tbody>
    </table>

   La timeline del video utilizza la stessa quantità di spazio disponibile sullo schermo utilizzata. Di conseguenza, quando ridimensionate il browser, i segmenti aggiunti mantengono la larghezza corretta.

   Ad esempio, le tre schermate seguenti utilizzano lo stesso video. La larghezza di ciascun segmento varia a seconda dell’impostazione Scala timeline.

   ![chlimage_1-23](assets/chlimage_1-129.png)

   Screenshot A

   La schermata A precedente mostra la visualizzazione predefinita di un video prodotto di 29 secondi. La scala della timeline è impostata sul valore predefinito di 5 secondi.

   ![chlimage_1-130](assets/chlimage_1-130.png)

   Screenshot B

   Nella schermata B sopra, il cursore Scala timeline è stato trascinato dal valore predefinito di 5 secondi a 3 secondi. Tenere presente che i timbri temporali della scala della linea temporale sono ora impostati a intervalli di 3 secondi.

   ![chlimage_1-25](assets/chlimage_1-131.png)

   Screenshot C

   Nella schermata C precedente, l’impostazione Scala timeline è stata spostata a 8 secondi. I segmenti che contengono miniature di prodotto si sono ridotti. Lo zoom out in questo modo è utile se si dispone di un video lungo e si desidera visualizzare una panoramica di più segmenti che normalmente rientrerebbero nella larghezza della pagina.

1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Per regolare l’ora di inizio e di fine di un segmento.

      Selezionate un segmento, quindi trascinate l’ovale blu iniziale o finale per regolare rispettivamente l’ora iniziale e finale. In base alle regolazioni apportate, il fotogramma video visualizzato passa alla posizione temporale appropriata nel video. Lo spostamento del segmento della timeline è limitato in base a eventuali segmenti adiacenti nella timeline. Il tempo minimo consentito per il segmento è di un secondo.

      Utilizzate i seguenti collegamenti di navigazione per controllare e perfezionare rapidamente i segmenti video:

      * Toccate l’ovale blu iniziale per cercare il video direttamente all’inizio del segmento.
      * Toccate l’ovale blu finale per cercare il video direttamente alla fine del segmento.
      * Toccate l’intero segmento per ripristinare la riproduzione video all’inizio di tale segmento

   ![chlimage_1-26](assets/chlimage_1-132.png)

   Riposizionamento della fine di un segmento della timeline

   * Per eliminare un segmento

      Selezionare l&#39;ultimo segmento nella timeline, quindi sulla barra degli strumenti toccare **[!UICONTROL Elimina segmento.]** Se sono selezionati due o più segmenti, la funzione Elimina segmento è disabilitata.

      Puoi eliminare solo l’ultimo segmento. Ad esempio, se si desidera eliminare tutti i segmenti sulla timeline, è necessario selezionare sempre l&#39;ultimo, quindi toccare **[!UICONTROL Elimina segmento.]**


1. Selezionate un segmento di tempo al quale desiderate associare una o più miniature.
1. A destra del video, toccate la scheda **[!UICONTROL Contenuto]**.
1. Nella scheda Contenuto, toccate **[!UICONTROL Seleziona risorse]**, quindi individuate e selezionate tutte le risorse di immagine che desiderate usare con il video. Le risorse selezionate vengono aggiunte al pannello Selettore risorse nella scheda Contenuto.

1. Nel selettore delle risorse sotto la scheda Contenuto, effettuate una delle seguenti operazioni:

   <table>
      <tbody>
        <tr>
        <td>Per associare una miniatura al segmento della timeline selezionato</td>
        <td><p>Toccate l’immagine nel pannello del selettore delle risorse a destra.</p> <p>Puoi aggiungere tutte le miniature desiderate a un segmento della timeline. Per ogni immagine selezionata, viene visualizzato un segno di spunta sull’immagine nel selettore delle risorse.</p> </td>
        </tr>
        <tr>
        <td>Per rimuovere una miniatura dal segmento della timeline selezionato</td>
        <td><p>Effettua una delle operazioni seguenti:</p>
          <ul>
          <li>Nel pannello del selettore delle risorse, toccate un’immagine con un segno di spunta per deselezionarla. La risorsa immagine viene rimossa dal segmento della timeline.<br /> </li>
          <li>Nel segmento della timeline selezionato, toccate un'immagine, quindi sulla barra degli strumenti, toccate <strong>Elimina prodotto</strong>.</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![Selettore risorse](assets/chlimage_1-133.png)

   Toccando un’immagine nel pannello del selettore delle risorse, questa viene aggiunta al segmento della timeline selezionato.

1. Seleziona una singola miniatura all&#39;interno di uno dei segmenti della cronologia, quindi tocca la scheda **[!UICONTROL Actions]**.
1. Effettua una delle operazioni seguenti:
   <table> 
    <tbody> 
      <tr> 
      <td>Per associare la miniatura selezionata a una visualizzazione rapida</td> 
      <td><p>In Tipo azione, toccare <strong>Quickview</strong>.</p> <p>Se siete un cliente AEM Sites  ed e-commerce:</p> 
       <ul> 
       <li>Il campo di testo Valore SKU è precompilato con lo SKU (Stock Keeping Unit) del prodotto selezionato, che è un identificatore univoco per ciascun prodotto o servizio distinto offerto. Questo viene popolato automaticamente quando l'immagine è associata a un prodotto in AEM Commerce.</li> 
       <li>Se lo SKU precompilato non è corretto, toccate o fate clic sull'icona del selettore prodotto (lente di ingrandimento) per aprire la pagina Seleziona prodotto. Toccate o fate clic sul prodotto che desiderate utilizzare, quindi toccate il segno di spunta nell'angolo superiore destro della pagina per tornare all'Editor video interattivo.</li> 
       </ul> <p> Se si è <em>not</em> un cliente AEM Sites o Ecommerce </p> 
       <ul> 
       <li>Vedere <a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">Identificazione delle variabili dei punti di attivazione</a>. Sarà necessario definire queste variabili. </li> 
       <li>Per impostazione predefinita, questo campo SKU utilizza il nome del file della risorsa immagine senza l’estensione. Se seguite una convenzione di denominazione standard per i file basati su SKU, in genere non sono necessarie ulteriori modifiche. </li> 
       <li>In caso contrario, modificate il valore predefinito e inserite il valore SKU corretto. Nel campo di testo Valore SKU, digitare lo SKU del prodotto (Stock Keeping Unit), che è un identificatore univoco per ogni prodotto o servizio distinto offerto. Il valore SKU immesso popola automaticamente la porzione variabile del modello Quickview in modo che il sistema sappia associare l’immagine toccata a una particolare visualizzazione Quickview dello SKU.</li> 
       </ul> <p>(Facoltativo) Se all'interno della visualizzazione rapida sono presenti altre variabili che è necessario utilizzare per identificare ulteriormente un prodotto, toccare <strong>Aggiungi variabile generica</strong>. Nel campo di testo, specificate una variabile aggiuntiva. Ad esempio, <code>category=Womens</code> è una variabile aggiunta.</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>Per associare l'immagine in miniatura selezionata a un collegamento ipertestuale</td> 
      <td><p>In Tipo azione, toccare <strong>Collegamento ipertestuale</strong>, quindi effettuare una delle seguenti operazioni:</p> 
       <ul> 
       <li>Se siete un cliente AEM Sites , toccate l'icona Selettore sito (cartella) per passare a una pagina Web. Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.</li> 
       <li>Se siete clienti indipendenti di contenuti multimediali dinamici, specificate nel campo HREF il percorso completo dell’URL di una pagina Web collegata.</li> 
       </ul> <p>Accertatevi di specificare se aprire il collegamento in una nuova scheda del browser o nella scheda corrente.</p> </td> 
      </tr> 
      <tr> 
      <td>Per associare l'immagine in miniatura selezionata a un frammento esperienza</td> 
      <td><p>In Tipo azione, toccate <strong>Frammento esperienza</strong>, quindi eseguite le seguenti operazioni:<p> 
       <ul> 
       <li>Se siete un cliente AEM Sites , toccate o fate clic sull’icona di ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza. Toccate o fate clic sul frammento esperienza da utilizzare, quindi toccate <strong>Seleziona </strong>nell'angolo superiore destro della pagina per tornare al pannello Azioni nella pagina precedente.<br /> Consulta Frammenti <a href="/help/sites-authoring/experience-fragments.md"> </a>esperienza.</li> 
      </ul> 
       <ul> 
       <li>Specificate la larghezza e l’altezza del frammento esperienza così come apparirà sul video.</li>
       </ul><strong>Nota</strong>: Gli strumenti di condivisione social media in Video interattivo non sono supportati quando incorporate il visualizzatore in un frammento esperienza. Per ovviare a questo problema, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.</p></tr>&lt;&gt; 
      <tr> 
      <td>Per modificare un'azione già assegnata a una miniatura</td> 
      <td>In un segmento della timeline, toccate una miniatura con un collegamento a catena a destra dell’etichetta di testo. Il collegamento a catena indica che vi è stata assegnata un'azione. Toccate la scheda <strong>Azioni</strong> per apportare le modifiche.</td> 
      </tr> 
      <tr> 
      <td>Per modificare l'etichetta di testo di una miniatura</td> 
      <td><p>Per impostazione predefinita, l'etichetta di testo utilizza il campo di metadati <code>Title</code> dell'immagine miniatura. Se <code>Title</code> non è presente, viene utilizzato il nome del file dell'immagine in miniatura, ma senza l'estensione.</p> <p>Per modificare l'etichetta di testo di un'immagine in miniatura, nella scheda <strong>Azioni </strong>, direttamente sotto la risorsa immagine visualizzata, immettete il testo desiderato. Vedere l'illustrazione seguente.</p> <p>La nuova etichetta di testo viene utilizzata solo dal lettore video stesso e dal testo della miniatura visualizzato nel segmento della timeline. La modifica dell'etichetta non influisce né sul campo dei metadati Titolo dell'immagine in miniatura né sul relativo nome file.</p> </td> 
      </tr> 
      <tr> 
      <td>Ripristino di una modifica apportata</td> 
      <td>Nell'angolo superiore destro della pagina, toccare <strong>Annulla</strong> o <strong>Ripristina</strong>.</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   All’immagine in miniatura viene aggiunta una nuova etichetta di testo.

1. Effettua una delle operazioni seguenti:

   * Ripetete i passaggi da 6 a 11 per aggiungere altre miniature ai segmenti della timeline nel video.
   * Passate al passaggio facoltativo 13.

1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * **[!UICONTROL Unisci segmento]** : puoi combinare due segmenti adiacenti (con o senza l’assegnazione di miniature di prodotto) in un unico segmento.

      Sulla timeline, toccate due o più segmenti contigui da unire in uno. Tenere presente che non esistono maniglie di trascinamento ovali blu sui due segmenti selezionati nell&#39;illustrazione seguente.

      Toccate **[!UICONTROL Unisci segmento]** sulla barra degli strumenti.
   ![chlimage_1-134](assets/chlimage_1-134.png)

   Unione di due segmenti selezionati di cinque secondi in un segmento di dieci secondi.

   * **[!UICONTROL Segmento]**  diviso: è possibile dividere un singolo segmento in due segmenti con un tempo uguale. Se al segmento sono già assegnate delle miniature di prodotto, queste vengono combinate nel segmento sinistro.

      Nella timeline, toccate un segmento da dividere a metà, quindi toccate **[!UICONTROL Dividi segmento]** sulla barra degli strumenti.

      Selezionando due o più segmenti, viene disattivata la funzione **[!UICONTROL Dividi segmento]**.
   ![chlimage_1-135](assets/chlimage_1-135.png)

   Suddivisione di un segmento selezionato di dieci secondi in due segmenti di cinque secondi ciascuno.

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Crea video interattivo]** viene visualizzato il nome del predefinito per visualizzatori attualmente selezionato usato con il video. Toccate il nome per selezionare un altro predefinito per visualizzatori.

   Ad esempio, il predefinito per visualizzatori `Shoppable_Video_light` consente di riprodurre il video con un&#39;area di visualizzazione bianca adiacente al video. Nell’area di visualizzazione vengono visualizzate le miniature selezionabili durante la riproduzione. Il predefinito per visualizzatori `Shoppable_Video_dark` consente di riprodurre il video con un&#39;area di visualizzazione nera adiacente al video.

   Se avete creato un predefinito per visualizzatori video interattivi personalizzato, lo vedrete anche nell’elenco dei predefiniti da cui potete scegliere.

   Al termine, toccare **[!UICONTROL Salva.]**

   >[!NOTE]
   Quando salvi il video interattivo, con esso viene salvato automaticamente un file associato `.vtt`. Il file `.vtt`viene salvato nella cartella principale `_VTT` di **[!UICONTROL Assets.]** Il file e la cartella sono necessari affinché il video interattivo possa essere riprodotto correttamente sul sito web. Non spostare, modificare o eliminare la cartella `_VTT` o il relativo contenuto.

1. Pubblicate il video interattivo. Con la pubblicazione viene creato il codice o l’URL da incorporare e da copiare e incollare nelle esperienze del sito Web.

   Se avete aggiunto interattività con le visualizzazioni rapide, usate solo il codice da incorporare; se avete aggiunto interattività con pagine Web con collegamenti ipertestuali, potete anche usare l’URL pubblicato. Tuttavia, il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.

   Consultate [Pubblicazione di risorse](publishing-dynamicmedia-assets.md).

   >[!NOTE]
   Per pubblicare un video acquistabile con Visualizzazioni rapide, accertatevi anche di pubblicare separatamente ciascuna risorsa immagine del video correlata dall’area di commercio.

   Dopo aver aggiunto i segmenti della timeline e pubblicato il video interattivo, potete aggiungerlo alla pagina di destinazione del sito Web esistente. Consultate [Integrazione di un video interattivo con il sito Web.](#integrating-an-interactive-video-with-your-website)

## Pubblicazione di risorse video interattive {#publishing-interactive-video-assets}

Per informazioni dettagliate sulla pubblicazione di risorse video interattive, consultate [Pubblicazione di risorse](/help/assets/publishing-dynamicmedia-assets.md).

## Integrazione di un video interattivo con il sito Web {#integrating-an-interactive-video-with-your-website}

Dopo aver caricato un video, aggiunto alcuni segmenti della timeline e pubblicato il video interattivo, potete ora aggiungerlo al sito Web esistente.

Se siete un cliente AEM Sites , potete aggiungere il video interattivo trascinando il componente Supporto interattivo sulla pagina. Vedere [Aggiunta di risorse multimediali dinamiche alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Se siete clienti indipendenti  AEM Assets, potete aggiungere manualmente il video interattivo al sito Web come descritto in questa sezione.

1. Copiate il codice o l’URL di incorporamento del video interattivo pubblicato.
Consultate [Incorporamento del visualizzatore video o di immagini in una pagina Web](/help/assets/embed-code.md).
Se avete aggiunto interattività con le visualizzazioni rapide, usate solo il codice da incorporare; se avete aggiunto interattività con pagine Web con collegamenti ipertestuali, potete anche usare l’URL pubblicato. Tuttavia, il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.

1. Nel codice della pagina Web della destinazione, identificate la posizione del video statico.
1. Rimuovete il video statico e sostituite il codice con il codice da incorporare o l’URL copiato da  AEM Assets, così come è.
Il codice da incorporare copiato è impostato per un ambiente reattivo, pertanto dovrebbe adattarsi automaticamente all’area precedentemente occupata dal video statico.

>[!NOTE]
A questo punto, se avete aggiunto interattività solo con pagine Web con collegamento ipertestuale, avete finito.
Tuttavia, se avete aggiunto interattività per attivare una visualizzazione rapida, le miniature adiacenti al video interattivo sono solo a scopo di visualizzazione; non sono ancora integrati con le viste Quickview esistenti. In tal caso, è ora necessario integrare il video interattivo con le visualizzazioni rapide esistenti sul sito Web.

**Esempio**

Esempio di utilizzo del sito Web demo:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

Si noti che si tratta di un codice di incorporamento video standard:

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

L&#39;integrazione è semplice come rimuovere il codice da incorporare video e sostituirlo con il codice da incorporare video interattivo da AEM. Il risultato è riportato nell’URL seguente. Anche se mostra un video interattivo presente sulla pagina, non è ancora integrato con le viste rapida esistenti:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html)

## Integrazione di un video interattivo con una visualizzazione rapida esistente {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
Questa attività si applica solo se siete clienti  AEM Assets indipendenti.

L’ultimo passaggio di questo processo consiste nell’integrare il video interattivo con un’implementazione esistente di Quickview utilizzata sul sito Web. Non esiste una soluzione all&#39;integrazione che funzioni per tutti i casi. Ogni implementazione della visualizzazione rapida è univoca. Di conseguenza, è necessario un approccio specifico che molto probabilmente implichi l&#39;assistenza di una persona IT front-end.

L’implementazione esistente di Quickview rappresenta in genere una catena di azioni correlate che si verificano sulla pagina Web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito Web.
1. Il codice front-end ottiene un URL Quickview basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta di AJAX utilizzando l&#39;URL ottenuto al punto 2.
1. La logica di back-end restituisce i dati o il contenuto della visualizzazione rapida corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto della visualizzazione rapida.
1. Facoltativamente, il codice front-end converte i dati Quickview caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l&#39;utente finale.

Queste chiamate potrebbero non rappresentare chiamate API pubbliche indipendenti che possono essere richiamate dalla logica della pagina Web da un passaggio arbitrario. Si tratta, invece, di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Allo stesso tempo, il video interattivo sostituisce il passaggio 1 e in parte il passaggio 2, quando un utente fa clic su una miniatura all’interno del video interattivo, tale interazione viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina Web che contiene tutti i dati delle miniature precedentemente aggiunti al AEM.

In un gestore eventi di questo tipo, il codice front-end effettua le seguenti operazioni:

* Consente di ascoltare un evento emesso dal video interattivo.
* Crea un URL di visualizzazione rapida basato sui dati delle miniature.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering della visualizzazione sullo schermo.

Inoltre, il visualizzatore per video interattivi supporta la modalità di funzionamento a schermo intero. L&#39;utente finale attiva le visualizzazioni rapide facendo clic su una miniatura senza uscire dallo schermo intero. Per ottenere questa funzionalità, modificate il codice front-end in modo che la finestra di dialogo modale Quickview sia collegata al contenitore del visualizzatore. Non aggiungete il BODY del documento o altri elementi di pagina Web non disponibili quando il visualizzatore è in modalità a schermo intero. Il codice che esegue questo processo deve ascoltare un altro callback del visualizzatore inviato dopo il caricamento del visualizzatore sulla pagina.

Il codice da incorporare restituito da AEM dispone già di un gestore eventi ready-to-use. È commentato come mostrato nel frammento di codice evidenziato seguente:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

Pertanto, è solo necessario rimuovere il commento al frammento di codice evidenziato qui sopra e sostituire il corpo del gestore fittizio con codice specifico per la pagina Web.

Nel codice da incorporare standard sono presenti due gestori di callback predefiniti: `quickViewActivate` e `initComplete`. Il gestore `quickViewActivate` viene attivato quando si fa clic su una miniatura nel visualizzatore. Utilizzatelo per integrare il visualizzatore con la logica di attivazione della visualizzazione rapida. Il gestore `initComplete` viene attivato una sola volta quando il visualizzatore viene caricato nella pagina. Questo handler viene utilizzato per regolare la posizione della finestra di dialogo Visualizzazione rapida nel DOM della pagina Web.

Il processo di creazione dell’URL di visualizzazione rapida è opposto al processo di identificazione delle variabili delle miniature di cui sopra. Utilizzando i nostri esempi di URL Quickview precedentemente identificati, potete vedere come l’URL Quickview è costruito in ogni caso:

<table>
  <tbody>
  <tr>
    <td><p>SKU singolo, trovato nella stringa di query</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>SKU singolo, trovato nel percorso URL</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa di query</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

L’ultimo passaggio per attivare l’URL di visualizzazione rapida e attivare il pannello di visualizzazione rapida richiede probabilmente l’assistenza di un esperto IT front-end del reparto IT. Essi hanno la capacità di sapere come attivare con precisione l’implementazione della visualizzazione rapida dal passaggio corretto, avendo un URL Quickview pronto all’uso.

Potete vedere come questi passaggi vengono applicati al sito Web dimostrativo per integrare completamente un video interattivo con il codice Quickview. In precedenza, in questo argomento, la struttura dell’URL di visualizzazione rapida era identificata come segue:

```xml
/datafeed/$CategoryId$-$SKU$.json
```

È facile ricostruire questo URL all&#39;interno del gestore `quickViewActivate` utilizzando i campi `categoryId` e `sku` disponibili nell&#39;oggetto `inData` passato al gestore tramite il codice del visualizzatore come illustrato di seguito:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Il sito Web dimostrativo sta attivando la finestra di dialogo Quickview utilizzando una semplice chiamata di funzione `loadQuickView()`. Questa funzione richiede un solo argomento, ovvero l&#39;URL dei dati di Quickview. L&#39;ultimo passaggio necessario per integrare il video interattivo è quindi aggiungere la seguente riga di codice al gestore `quickViewActivate`:

```xml
loadQuickView(quickViewUrl);
```

Infine, verificate che la finestra di dialogo Quickview sia associata all’elemento contenitore del visualizzatore. Il codice di incorporamento predefinito fornisce esempi di passaggi per ottenere questa funzionalità. Per ottenere un riferimento all’elemento contenitore del visualizzatore, potete usare le seguenti righe di codice:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

Dove `inner_container` è un riferimento a un elemento `DIV` gestito dal visualizzatore. La finestra di dialogo deve essere un elemento secondario di tale `DIV`.

I passaggi per individuare l&#39;elemento della finestra di dialogo modale e collegarlo al contenitore di cui sopra sono specifici per le maiuscole e le minuscole. Anche in questo caso, potete ottenere l&#39;aiuto dello sviluppatore front-end che abbia familiarità con l&#39;implementazione di Quickview necessaria.

Nel caso del sito Web di esempio, la finestra di dialogo modale Quickview viene implementata come `DIV` con l&#39;ID quickview-modale collegato direttamente al documento `BODY`. Di conseguenza, il codice per spostare tale finestra di dialogo nel contenitore del visualizzatore è semplice come segue:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

Il codice sorgente completo è il seguente:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

Il sito Web della demo finale con il video interattivo completamente integrato si presenta come segue:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

## Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

Vedere [Uso delle visualizzazioni rapide per creare pop-up personalizzati](/help/assets/custom-pop-ups.md).
