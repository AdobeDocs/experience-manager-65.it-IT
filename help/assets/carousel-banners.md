---
title: Banner a carosello
description: Scopri come utilizzare i banner a carosello in Dynamic Medie
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Carousel Banners
role: User, Admin
exl-id: 53d34d3a-ecb6-4fa0-9665-60d21f48021e
solution: Experience Manager, Experience Manager Assets
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '4677'
ht-degree: 3%

---

# Banner a carosello{#carousel-banners}

I banner carosello consentono agli addetti al marketing di promuovere la conversione dei contenuti creando facilmente contenuti promozionali a rotazione interattivi e distribuendoli a qualsiasi schermo.

La creazione e la modifica dei contenuti visualizzati nei banner promozionali può richiedere tempo, limitando la possibilità di pubblicare rapidamente nuovi contenuti o renderli più mirati. I banner a carosello consentono di creare o modificare rapidamente i banner rotanti. È possibile aggiungere interattività, come il collegamento di hotspot ai dettagli dei prodotti o alle risorse correlate, e distribuirli su qualsiasi schermo, consentendo di immettere nuovi contenuti promozionali sul mercato più rapidamente.

I banner a carosello sono indicati da un banner con la parola **[!UICONTROL CAROUSELSET]**

![chlimage_1-438](assets/chlimage_1-438.png)

Sul sito web, un banner a carosello può essere visualizzato come segue:

![chlimage_1-439](assets/chlimage_1-439.png)

Qui puoi navigare tra le immagini (facendo clic sui numeri). Inoltre, le diapositive ruotano automaticamente in base a un intervallo di tempo personalizzabile. Le immagini aggiunte nei banner carosello supportano sia punti attivi che mappe immagine, dove gli utenti possono selezionare o visitare un collegamento ipertestuale o accedere a una finestra Quickview.

In questo esempio, un utente ha toccato o fatto clic su una mappa immagine e ha effettuato l&#39;accesso alla finestra Quickview per i guanti:

![chlimage_1-440](assets/chlimage_1-440.png)

## Guarda come vengono creati i banner a carosello {#watch-how-carousel-banners-are-created}

Riproduci una procedura dettagliata su [come vengono creati i banner a carosello](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)(10 minuti e 33 secondi). Scopri anche come visualizzare in anteprima, modificare e distribuire banner carosello.

>[!NOTE]
>
>Gli utenti non amministratori devono essere aggiunti al gruppo **[!UICONTROL `dam-users`]** per poter creare o modificare i banner a carosello. In caso di problemi durante la creazione o la modifica, contattare l&#39;amministratore di sistema che potrà aggiungerti al gruppo **[!UICONTROL `dam-users`]**.

## Guida introduttiva: Banner a carosello {#quick-start-carousel-banners}

Per iniziare subito a usare i banner a carosello:

1. [Identificare le variabili del punto attivo e della mappa immagine](#identifying-hotspot-and-image-map-variables) (solo per i clienti che utilizzano Experience Manager Assets + Dynamic Medie)

   Inizia identificando le variabili dinamiche utilizzate dall’implementazione Quickview esistente, in modo da poter immettere correttamente gli hotspot e i dati della mappa immagine durante il processo di creazione del banner a carosello in Adobe Experience Manager Assets.

   >[!NOTE]
   >
   >Se sei un cliente Experience Manager Sites o e-commerce, puoi utilizzare la funzione incorporata per passare alle pagine dei prodotti e cercare le SKU (Stock Keeping Unit) esistenti nel catalogo dei prodotti. Non è necessario immettere manualmente le variabili del punto attivo o della mappa immagine. Vedi le informazioni su [configurazione di eCommerce](/help/commerce/cif-classic/administering/generic.md).
   >
   >
   >Se sei un cliente di Experience Manager Assets e Dynamic Medie, immetti manualmente i dati per gli hotspot e le mappe immagine, quindi integri l’URL pubblicato o il codice da incorporare con il sistema di gestione dei contenuti di terze parti.

1. Facoltativo: se necessario, [crea un predefinito visualizzatore per set carosello](/help/assets/managing-viewer-presets.md).

   Se sei un amministratore, puoi personalizzare il comportamento e l’aspetto del carosello creando un predefinito visualizzatore Carosello personalizzato. Il vantaggio principale è che puoi riutilizzare questo predefinito visualizzatore personalizzato per più caroselli di immagini. Tuttavia, gli utenti possono personalizzare facoltativamente il comportamento e l’aspetto del carosello direttamente durante la creazione dello stesso. Questo metodo è l’approccio preferito quando si desidera un progetto specifico per un determinato carosello.

1. [Carica un banner immagine](#uploading-image-banners).

   Carica i banner immagine da rendere interattivi.

1. [Crea set carosello](#creating-carousel-sets).

   In Set caroselli di immagini, gli utenti possono navigare tra le immagini dei banner e selezionare punti attivi o mappe immagine per accedere al contenuto pertinente.

   Per creare un set carosello in Assets, seleziona **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL Set carosello]**. Aggiungi risorse a ciascuna diapositiva e seleziona **[!UICONTROL Salva]**. Inoltre, puoi modificare l’aspetto e il comportamento del carosello direttamente nell’editor.

1. [Aggiungi punti attivi o mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).

   Aggiungi uno o più punti attivi o mappe immagine a un banner immagine e associali a un&#39;azione, ad esempio un collegamento, una visualizzazione rapida o un frammento esperienza. Dopo aver aggiunto punti attivi o mappe immagine, completa questa attività pubblicando il set carosello. La pubblicazione crea il codice da incorporare che puoi utilizzare per copiare e applicare alla pagina di destinazione del sito web.

   Vedere [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners) - Facoltativo Se lo desideri, puoi visualizzare una rappresentazione del set carosello e testarne l’interattività.

1. [Banner a carosello Publish](#publishing-carousel-banners).

   Pubblichi un set carosello come faresti con una risorsa. In Assets, passa al set carosello, selezionalo e seleziona **[!UICONTROL Publish]**. La pubblicazione di un set carosello attiva l’URL e la stringa di incorporamento.

1. Effettua una delle operazioni seguenti:

   * [Aggiungi un banner carosello alla pagina del tuo sito Web](#adding-a-carousel-banner-to-your-website-page) Puoi aggiungere l&#39;URL del banner carosello o il codice da incorporare copiato nella pagina del sito Web.

      * [Integrare il banner del carosello con un Quickview esistente](#integrating-the-carousel-banner-with-an-existing-quickview). Se utilizzi un sistema di gestione dei contenuti web di terze parti, devi integrare il nuovo banner carosello con l’implementazione Quickview esistente sul tuo sito web.

   * [Aggiungi un banner carosello al tuo sito Web nell&#39;Experience Manager](/help/assets/adding-dynamic-media-assets-to-pages.md) Se sei un cliente Experience Manager Sites puoi aggiungere il set carosello direttamente alla pagina nell&#39;Experience Manager, utilizzando il componente File multimediali interattivi.

Per modificare i set carosello, vedi [modifica dei set carosello](#editing-carousel-sets). Inoltre, puoi visualizzare e modificare [le proprietà del set carosello](manage-assets.md#editing-properties).

## Identificare le variabili hotspot e mappa immagine {#identifying-hotspot-and-image-map-variables}

Inizia identificando le variabili dinamiche utilizzate dall’implementazione Quickview esistente, in modo da poter immettere correttamente gli hotspot o i dati della mappa immagine durante il processo di creazione del set carosello in Experience Manager Assets.

Quando aggiungi punti attivi o mappe immagine a un&#39;immagine del banner in Experience Manager Assets, assegna una SKU e variabili aggiuntive facoltative a ciascun punto attivo o mappa immagine. Tali variabili vengono utilizzate in un secondo momento per far corrispondere i punti attivi o le mappe immagine con il contenuto Quickview.

>[!NOTE]
>
>Se sei un cliente Experience Manager Sites e/o Experience Manager di e-commerce, salta questo passaggio. Non è necessario identificare manualmente le variabili del punto attivo o della mappa immagine; puoi utilizzare l’integrazione con e-commerce per l’integrazione con il prodotto. Vedi le informazioni su [configurazione di eCommerce](/help/commerce/cif-classic/administering/generic.md). Inoltre, puoi utilizzare il componente Interattivo e aggiungerlo alla pagina web.
>
>Se sei un cliente Experience Manager Assets o Media, pubblichi l’URL o il codice da incorporare, quindi esegui l’integrazione con il sistema di gestione dei contenuti di terze parti e identifica manualmente i punti attivi e le mappe immagine.

È importante identificare correttamente il numero e il tipo di variabili da associare ai dati del punto attivo o della mappa immagine. Ogni punto attivo o mappa immagine aggiunta a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo inequivocabile il prodotto nel sistema back-end esistente. Allo stesso tempo, ogni punto attivo o mappa immagine non deve includere più dati del necessario. Il motivo è che questo renderebbe il processo di immissione dei dati eccessivamente complesso e la gestione dei punti attivi o delle mappe immagine in corso più soggetta a errori.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati del punto attivo o della mappa immagine.

A volte è sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione Quickview esistente. È probabile che conoscano il set minimo di dati necessari per identificare Quickview nel sistema. Tuttavia, di solito è anche possibile semplicemente analizzare il comportamento esistente del codice front-end.

La maggior parte delle implementazioni Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, toccando un pulsante **[!UICONTROL Quickview]**.
* Il sito web invia una richiesta Ajax al backend per caricare i dati o il contenuto Quickview, se necessario.
* I dati Quickview vengono tradotti nel contenuto in preparazione al rendering sulla pagina web.
* Infine, il codice front-end riproduce visivamente tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito web esistente in cui è implementata la funzione Quickview. Attiva Quickview e acquisisci l’URL Ajax inviato dalla pagina web per caricare i dati o il contenuto Quickview.

In genere non è necessario utilizzare strumenti di debug specifici. I browser web moderni dispongono di web inspector che svolgono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser Web che includono i controlli Web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere F12 (Windows) o Command-Option-I (Mac) per aprire il pannello Strumenti per sviluppatori e quindi selezionare la scheda Rete.
* In Firefox, è possibile attivare il plug-in Firebug premendo F12 (Windows) o Command-Option-I (Mac) e utilizzando la relativa scheda Net, oppure è possibile utilizzare lo strumento integrato Inspector e la relativa scheda Rete.

Quando il monitoraggio della rete è attivato nel browser, attiva Quickview sulla pagina.

Ora trova l’URL Ajax di Quickview nel registro di rete e copia l’URL registrato per l’analisi futura. Di solito, quando si attiva Quickview, vengono inviate numerose richieste al server. In genere, l’URL Ajax di Quickview è uno dei primi dell’elenco. Ha una porzione o un percorso di stringa di query complesso e il relativo tipo MIME di risposta è `text/html`, `text/xml` o `text/javascript`.

Durante questo processo, è importante visitare diverse aree del sito web, con diverse categorie e tipi di prodotti. Il motivo è che gli URL Quickview hanno parti comuni per una determinata categoria di siti web, ma cambiano solo se visiti un’area diversa del sito web.

Nel caso più semplice, l’unica parte variabile nell’URL di Quickview è lo SKU del prodotto. In questo caso, il valore SKU è l&#39;unico dato necessario per aggiungere punti attivi o mappe immagine all&#39;immagine del banner.

Tuttavia, in casi complessi, l’URL Quickview contiene elementi diversi che differiscono oltre allo SKU, come l’ID categoria, il codice colore e il codice dimensione. In questi casi, ogni elemento è una variabile separata nella definizione del punto attivo o della mappa immagine nella funzione del banner del carosello.

Prendi in considerazione i seguenti esempi di URL Quickview e le variabili hotspot o mappa immagine risultanti:

<table>
 <tbody>
  <tr>
   <td>Singolo SKU, trovato nella stringa di query.</td>
   <td><p>Gli URL registrati di Quickview includono:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L'unica parte variabile nell'URL è il valore del parametro della stringa di query <code>productId=</code> ed è chiaramente un valore SKU. Pertanto, i punti attivi o le mappe immagine richiedono solo campi SKU compilati con valori come <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>Singolo SKU, trovato nel percorso URL.</td>
   <td><p>Gli URL registrati di Quickview includono:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell'ultima parte del percorso e diventa il valore SKU dei punti attivi/mappe immagine:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID categoria nella stringa query.</td>
   <td><p>Gli URL registrati di Quickview includono:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU è archiviato nel parametro <code>prodId</code> e l'ID categoria nel parametro <code>category=</code>.</p> <p>Di conseguenza, le definizioni del punto attivo/mappa immagine sono coppie. ovvero un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
     <li><p>Lo SKU è <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
     <li><p>Lo SKU è <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
     <li><p>Lo SKU è <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Carica banner immagine {#uploading-image-banners}

Se hai già caricato le immagini che desideri utilizzare, passa al passaggio successivo, [Crea set carosello](#creating-carousel-sets). Nota: le immagini utilizzate nel carosello devono essere caricate dopo l’abilitazione di Dynamic Medie.

Per caricare i banner immagine, consulta [Caricare le risorse](/help/assets/manage-assets.md).

## Creare set carosello {#creating-carousel-sets}

>[!NOTE]
>
>Gli utenti non amministratori devono essere aggiunti al gruppo **[!UICONTROL `dam-users`]** per poter creare o modificare i banner a carosello. In caso di problemi durante la creazione o la modifica, contattare l&#39;amministratore di sistema che potrà aggiungerti al gruppo **[!UICONTROL `dam-users`]**.

**Per creare set carosello:**

1. In Assets, passa alla cartella in cui desideri creare il set carosello e vai a **[!UICONTROL Crea]** > **[!UICONTROL Set carosello]**.
1. Nella pagina dell&#39;editor di banner per carosello, seleziona **[!UICONTROL Tocca per aprire il selettore risorse]** per selezionare l&#39;immagine per la prima diapositiva.

   Nella pagina dell’editor di banner a carosello, effettua una delle seguenti operazioni:

   * Nell&#39;angolo superiore sinistro della pagina, selezionare l&#39;icona **[!UICONTROL Aggiungi diapositiva]**.

   * Nella parte centrale della pagina, seleziona **[!UICONTROL Tocca per aprire il selettore risorse]**.

   Seleziona per selezionare le risorse da includere nel set carosello. Le risorse selezionate dispongono di un’icona a forma di segno di spunta. Al termine, vicino all&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando o facendo clic su **[!UICONTROL Invio]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Selezionare il filtro e quindi l&#39;icona **[!UICONTROL Filtro]** sulla barra degli strumenti. Per modificare la visualizzazione, tocca l’icona Visualizza e fai clic su **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a elenco]**.

   Per ulteriori informazioni, vedere [Utilizzare i selettori](/help/assets/working-with-selectors.md).

1. Continuate ad aggiungere diapositive fino ad aggiungere tutte le immagini da ruotare nel set carosello.
1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Se necessario, trascinare la diapositiva per riordinare le immagini nell&#39;elenco.
   * Per eliminare un&#39;immagine, selezionarla, quindi selezionare **[!UICONTROL Elimina diapositiva]** sulla barra degli strumenti.

   * Per applicare un predefinito, seleziona l’elenco a discesa dei predefiniti nell’angolo superiore destro della pagina, quindi seleziona un predefinito da applicare al set contemporaneamente.

   Per eliminare una diapositiva, selezionarla, quindi sulla barra degli strumenti selezionare **[!UICONTROL Elimina diapositiva]**. Per spostare una diapositiva, selezionate l&#39;icona Riordina (Reorder), quindi tenete premuto e spostate nella posizione desiderata.

1. Dopo aver aggiunto le immagini nelle diapositive, è possibile aggiungere un punto attivo, una mappa immagine o entrambi all&#39;immagine. Consulta [Aggiungere punti attivi o mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
1. Puoi modificare la progettazione visiva e il comportamento dei set carosello. Seleziona le schede **[!UICONTROL Comportamento]** e **[!UICONTROL Aspetto]** e regola la modalità di visualizzazione del banner del carosello o il comportamento di componenti specifici. Per ulteriori informazioni sull&#39;utilizzo dell&#39;editor visualizzatore, vedere [Gestione predefiniti visualizzatore](/help/assets/viewer-presets.md).

   >[!NOTE]
   >
   >Per i banner a carosello, è possibile regolare quanto segue:
   >
   >    * Durata di visualizzazione di un’immagine. Per impostazione predefinita, ogni immagine viene visualizzata per 9 secondi.
   >    * Animazione. Per impostazione predefinita, ogni transizione di diapositiva è una dissolvenza. Potete cambiare questa transizione in una diapositiva.
   >    * Stile dei pulsanti. Gli utenti possono ruotare tra i banner toccando ogni punto o numero. È possibile modificare la posizione e le dimensioni dei pulsanti degli indicatori impostati (e se sono numerici o con uno stile punteggiato).
   >    * Modifica lo stile di evidenziazione di una mappa immagine o dell’icona utilizzata per gli hotspot.
   >    * Prima di modificare un predefinito visualizzatore, scegliete lo stile su cui basare il predefinito. Se non si sceglie uno stile, quando si inizia a modificare il predefinito visualizzatore, tutte le modifiche vengono perse se si decide di passare a un predefinito diverso.
   >
   >Per istruzioni dettagliate e ulteriori informazioni sull&#39;editor visualizzatore, vedere [Considerazioni speciali sui banner a carosello](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset).

   Puoi anche visualizzare in anteprima come verrà visualizzato il banner del carosello. Vedi [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners).

1. Al termine, seleziona **[!UICONTROL Salva]**.

## Aggiunta di punti attivi o mappe immagine a un banner immagine {#adding-hotspots-or-image-maps-to-an-image-banner}

Puoi aggiungere punti attivi o mappe immagine a un banner utilizzando l’editor di set carosello.

Quando aggiungete punti attivi o mappe immagine, potete definirli come una visualizzazione a comparsa Quickview, come un collegamento ipertestuale o un frammento di esperienza.

Vedi [Frammento esperienza](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Gli strumenti di condivisione per social media nel banner carosello non sono supportati quando si incorpora il visualizzatore in un frammento di esperienza.
>
>Per risolvere questo problema, puoi utilizzare o creare predefiniti visualizzatore che non dispongono di strumenti per la condivisione sui social media. Tali predefiniti visualizzatore consentono di incorporarli correttamente in Frammenti esperienza.

Quando aggiungi punti attivi o mappe immagine a un&#39;immagine, ricorda di salvare i tuoi dati. Le opzioni Annulla e Ripristina, posizionate nell&#39;angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione del banner carosello, puoi facoltativamente utilizzare Anteprima per visualizzare una rappresentazione dell’aspetto del banner ai clienti.

Vedi [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners).

>[!NOTE]
>
>Quando si aggiungono punti attivi a un&#39;immagine in una [Immagine interattiva](/help/assets/interactive-images.md) o un banner a carosello, le informazioni sui punti attivi vengono memorizzate nella stessa posizione di metadati. Tale posizione è relativa alla posizione dell&#39;immagine, indipendentemente dal fatto che si tratti di un&#39;immagine interattiva o di un banner a carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai dati dei punti attivi definiti, in entrambi i visualizzatori.
>
>Tieni presente, tuttavia, che i banner a carosello supportano le mappe immagine sulle immagini che possono anche contenere punti attivi, diversamente da un’immagine interattiva. Tieni presente questa regola se intendi creare un’immagine interattiva o un banner a carosello che utilizza la stessa immagine. Valuta la possibilità di creare immagini interattive e banner a carosello utilizzando copie separate della stessa immagine.

>[!NOTE]
>
>Se si modificano immagini interattive con punti attivi e si ritaglia l&#39;immagine, questi vengono rimossi.

Vedi anche [Aggiungere mappe immagine](/help/assets/image-maps.md).

**Per aggiungere punti attivi o mappe immagine a un banner immagine:**

1. Da Assets, individua il set carosello che desideri rendere interattivo.
1. Seleziona il set carosello e seleziona **[!UICONTROL Modifica]**. Viene aperto l’Editor visualizzatore carosello.
1. Selezionare la diapositiva da rendere interattiva.
1. Nell&#39;angolo superiore sinistro della pagina, selezionare **[!UICONTROL Punto attivo]** o **[!UICONTROL Mappa immagine]**.
1. Effettuare una delle seguenti operazioni:

   * Per punti attivi: sull&#39;immagine, seleziona la posizione in cui desideri visualizzare il punto attivo.
   * Per le mappe immagine: Sull’immagine, seleziona, quindi trascina dall’alto a sinistra verso il basso a destra per creare l’area della mappa immagine. È possibile regolare le dimensioni della mappa immagine trascinando gli angoli.

   Se necessario, trascina il punto attivo o la mappa immagine in una nuova posizione. Aggiungi altri punti attivi o mappe immagine in base alle esigenze.

   Per eliminare un punto attivo o una mappa immagine, seleziona la scheda **[!UICONTROL Azioni]**. Seleziona il nome del punto attivo o della mappa immagine da rimuovere dall’intestazione **[!UICONTROL Mappe e punti attivi]** del menu a discesa **[!UICONTROL Tipo selezionato]**. Seleziona l&#39;icona **[!UICONTROL Elimina]** accanto al menu, quindi seleziona **[!UICONTROL Elimina]**.

1. Nel campo di testo Nome digitare il nome del punto attivo o della mappa immagine. Questo nome viene visualizzato anche nell&#39;elenco a discesa **[!UICONTROL Mappe e punto attivo]**. Specificando un nome è facile identificare il punto attivo o la mappa immagine se si decide di modificarlo in futuro.
1. Effettua una delle seguenti operazioni nella scheda **[!UICONTROL Azioni]**:

   * Selezionare **[!UICONTROL Quickview]**.

      * Se sei un cliente di Experience Manager Sites e Ecommerce, seleziona l’icona del selettore prodotti (lente di ingrandimento) per aprire la pagina Seleziona prodotto. Seleziona il prodotto da utilizzare, quindi fai clic sul segno di spunta nell’angolo superiore destro della pagina per tornare all’editor di banner a carosello.
      * Se non sei un cliente Experience Manager Sites o e-commerce

         * Se vuoi definire queste variabili, consulta [Identificare le variabili del punto attivo](#identifying-hotspot-and-image-map-variables).
         * Quindi, immetti manualmente il valore SKU. Nel campo di testo Valore SKU digitare la SKU (Stock Keeping Unit) del prodotto, che rappresenta un identificatore univoco per ogni prodotto o servizio specifico offerto. Il valore SKU immesso popola automaticamente la parte variabile del modello Quickview in modo che il sistema sappia associare il punto attivo toccato alla visualizzazione rapida di una particolare SKU.
         * (Facoltativo) Se in Quickview sono presenti altre variabili che è necessario utilizzare per identificare ulteriormente un prodotto, selezionare **[!UICONTROL Aggiungi variabile generica]**. Nel campo di testo, specifica una variabile aggiuntiva. Ad esempio, category=Mens è una variabile aggiunta.

         * Per ulteriori informazioni, vedere [Utilizzare i selettori](/help/assets/working-with-selectors.md).

   * Seleziona **[!UICONTROL Collegamento ipertestuale]**.

      * Se sei un cliente di Experience Manager Sites, seleziona l’icona Selettore siti (cartella) per passare a un URL.

        >[!NOTE]
        >
        >Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a pagine Experience Manager Sites.

      * Se si è clienti autonomi, specificare il percorso URL completo di una pagina Web collegata nel campo di testo HREF.

   Assicurati di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Per ulteriori informazioni, vedere [Utilizzo dei selettori](/help/assets/working-with-selectors.md).

   * Seleziona **[!UICONTROL Frammento esperienza]**.

      * Se sei un cliente di Experience Manager Sites, seleziona l’icona Ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza. Seleziona il frammento di esperienza da utilizzare, quindi seleziona **[!UICONTROL Seleziona]** nell&#39;angolo superiore destro della pagina per tornare alla pagina di gestione dei punti attivi.
Vedi [Frammenti esperienza](/help/sites-authoring/experience-fragments.md).

      * Specifica la larghezza e l&#39;altezza del frammento di esperienza così come viene visualizzato sul banner.

        >[!NOTE]
        >
        >Gli strumenti di condivisione per social media nel banner carosello non sono supportati quando si incorpora il visualizzatore in un frammento di esperienza.
        >
        >Per risolvere questo problema, crea predefiniti visualizzatore che non dispongono di strumenti per la condivisione sui social media. Tali predefiniti visualizzatore consentono di incorporarli correttamente in Frammenti esperienza.

   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   Puoi anche visualizzare in anteprima come verrà visualizzato il banner del carosello. Vedere [(facoltativo) Anteprima dei banner carosello](#optional-previewing-carousel-banners).

1. Seleziona **[!UICONTROL Salva]**.
1. Publish il set carosello. La pubblicazione crea il codice o l’URL da incorporare che puoi utilizzare nella pagina del sito web. Se sei un cliente di Experience Manager Sites, puoi aggiungere il set del carosello direttamente alla pagina web.

   Consulta [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md).

   Consulta [Aggiunta di un set carosello alla pagina di destinazione del tuo sito Web](#adding-a-carousel-banner-to-your-website-page)

## Modifica set carosello {#editing-carousel-sets}

>[!NOTE]
>
>Gli utenti non amministratori devono essere aggiunti al gruppo **[!UICONTROL `dam-users`]** per poter creare o modificare i banner a carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all&#39;amministratore di sistema che potrà aggiungerti al gruppo **[!UICONTROL dam-users]**.

Puoi eseguire varie attività di modifica sui set carosello, come le seguenti:

* Aggiungere diapositive a un set carosello. Vedi anche [Utilizzare i selettori](/help/assets/working-with-selectors.md).
* Riordinare le diapositive nel set carosello.
* Elimina le risorse nel set carosello.
* Applica un predefinito visualizzatore.
* Elimina il set carosello.
* Aggiungi o modifica gli hotspot e le mappe immagine. Vedi anche [Utilizzare i selettori](/help/assets/working-with-selectors.md).

**Per modificare i set carosello:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa Set carosello, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita).
   * Passa il puntatore del mouse su una risorsa Set carosello, seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi seleziona **[!UICONTROL Modifica]** sulla barra degli strumenti.

   * Seleziona una risorsa Set carosello, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita) nell&#39;angolo superiore sinistro della pagina.

1. Per modificare il set carosello, effettuate una delle seguenti operazioni:

   * Per aggiungere una diapositiva, seleziona l&#39;icona **[!UICONTROL Aggiungi diapositiva]**, quindi individua la risorsa da aggiungere alla diapositiva e seleziona il segno di spunta.
   * Per riordinare le diapositive, trascinare una diapositiva in una nuova posizione (selezionare l&#39;icona Riordina per spostare gli elementi).
   * Per aggiungere un punto attivo o una mappa immagine, seleziona le icone del punto attivo o della mappa immagine e vedi [aggiunta di punti attivi e mappe immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
   * Per modificare l&#39;aspetto o il comportamento del set carosello, selezionare la scheda **[!UICONTROL Aspetto]** o **[!UICONTROL Comportamento]**, quindi impostare le opzioni desiderate.
   * Per modificare punti attivi o mappe immagine, nella diapositiva appropriata, seleziona un punto attivo o una mappa immagine e cambia come necessario nella scheda **[!UICONTROL Azioni]**.
   * Per eliminare una diapositiva, selezionarla, quindi selezionare **[!UICONTROL Elimina diapositiva]** sulla barra degli strumenti.
   * Per applicare un predefinito, seleziona l&#39;elenco a discesa **[!UICONTROL Predefinito]** nell&#39;angolo superiore destro della pagina, quindi seleziona un predefinito visualizzatore.
   * Per eliminare un intero set carosello, passare al set carosello, selezionarlo, quindi selezionare **[!UICONTROL Elimina]**.

   >[!NOTE]
   >
   >Se si modificano immagini interattive con punti attivi e si ritaglia l&#39;immagine, questi vengono rimossi.
   >
   >

## (Facoltativo) Anteprima dei banner a carosello {#optional-previewing-carousel-banners}

Puoi utilizzare Anteprima per vedere come il banner del carosello viene visualizzato dai clienti e per testare gli hotspot dei banner e le mappe immagine per assicurarti che si comportino come previsto.

Quando sei soddisfatto del banner del carosello, puoi pubblicarlo.
Consulta [Incorporazione di un visualizzatore di video o immagini in una pagina Web](/help/assets/embed-code.md).
Consulta [Collegamento degli URL all&#39;applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a pagine Experience Manager Sites.
Consulta [Aggiunta di Dynamic Medie Assets alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).

Puoi visualizzare in anteprima i banner carosello dall&#39;Editor carosello (metodo preferito) o dall&#39;elenco **[!UICONTROL Visualizzatori]**.

**Per visualizzare in anteprima i banner del carosello:**

1. In **[!UICONTROL Assets]**, passa a un banner carosello esistente creato e seleziona per aprirlo.
1. Seleziona **[!UICONTROL Modifica]**.
1. Nell’elenco dei predefiniti visualizzatore nell’angolo destro della barra degli strumenti, seleziona un visualizzatore per visualizzare in anteprima il banner del carosello.

   ![elenco a discesa experience_fragment-carouselbanner-viewer](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Selezionare **[!UICONTROL Anteprima]**.
1. Seleziona gli hotspot o le mappe immagine sull&#39;immagine in modo da poter testare le azioni associate.

**Per visualizzare in anteprima i banner a carosello dall&#39;elenco dei visualizzatori:**

1. In **[!UICONTROL Assets]**, passa a un banner carosello esistente creato e seleziona per aprirlo.
1. Seleziona l’icona Contenuto nell’angolo in alto a sinistra della pagina Anteprima.
1. Nell&#39;elenco **[!UICONTROL Visualizzatori]** nel pannello sul lato sinistro della pagina, seleziona il nome del predefinito visualizzatore banner a carosello che desideri utilizzare.
1. Seleziona gli hotspot o le mappe immagine sull&#39;immagine in modo da poter testare le azioni associate.

## Banner a carosello Publish {#publishing-carousel-banners}

Publish il carosello in modo da poterlo utilizzare. La pubblicazione di un set carosello attiva l’URL e il codice di incorporamento. Pubblica inoltre il carosello sul cloud Dynamic Medie, integrato con una rete CDN per una distribuzione scalabile e performante.

>[!NOTE]
>
>Se utilizzi un’immagine interattiva esistente con punti attivi per il banner carosello, devi pubblicarla separatamente dopo aver pubblicato il banner.
>
>Inoltre, se modifichi un’immagine interattiva pubblicata preesistente utilizzata in un banner carosello, devi pubblicare l’immagine interattiva prima che le modifiche vengano applicate al banner stesso.

Consulta [Publish Dynamic Medie Assets](/help/assets/publishing-dynamicmedia-assets.md) per informazioni su come pubblicare i banner a carosello.

## Aggiungi un banner carosello alla pagina del tuo sito web {#adding-a-carousel-banner-to-your-website-page}

Dopo aver caricato le immagini del banner per creare un carosello, aggiunto punti attivi e/o mappe immagine al banner e pubblicato il set di carosello, ora puoi aggiungerlo alla pagina del sito web esistente.

>[!NOTE]
>
>Se sei un cliente di Experience Manager Sites, puoi aggiungere il banner del carosello direttamente alla pagina trascinando il componente File multimediali interattivi nella pagina. Consulta [Aggiungere risorse Dynamic Medie alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).

Tuttavia, se sei un cliente di risorse di Experience Manager autonomo, puoi aggiungere manualmente il banner a carosello alla pagina di destinazione del sito web come descritto in questa sezione.

1. Copia il codice di incorporamento del set carosello pubblicato.
Vedi [Incorporare il video o il visualizzatore di immagini in una pagina Web](/help/assets/embed-code.md).

1. Aggiungi alla pagina web il codice da incorporare copiato da Experience Manager Assets.
Il codice di incorporamento copiato è reattivo, pertanto deve rientrare automaticamente nell’area di incorporamento della pagina.

## Integrare il banner del carosello con un Quickview esistente {#integrating-the-carousel-banner-with-an-existing-quickview}

>[!NOTE]
>
>Questo passaggio è valido solo per i clienti Experience Manager Assets autonomi.

L’ultimo passaggio di questo processo è l’integrazione del banner a carosello con un’implementazione Quickview esistente sul sito web. Ogni implementazione Quickview è unica ed è necessario un approccio specifico che coinvolga l&#39;assistenza di un responsabile IT front-end.

L’implementazione Quickview esistente rappresenta in genere una catena di azioni correlate che si verificano sulla pagina web nell’ordine seguente:

1. Un utente attiva un elemento nell’interfaccia utente del sito web.
1. Il codice front-end ottiene un URL Quickview basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto nel passaggio 2.
1. La logica di back-end restituisce i dati o il contenuto Quickview corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto Quickview.
1. Facoltativamente, il codice front-end converte i dati Quickview caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l’utente finale.

Queste chiamate non rappresentano chiamate API pubbliche indipendenti che possono essere chiamate dalla logica della pagina web da un passaggio arbitrario. Si tratta invece di una chiamata concatenata in cui ogni passaggio successivo è nascosto nell’ultima fase (callback) del passaggio precedente.

Allo stesso tempo in cui il banner del carosello sostituisce il passaggio 1 e parzialmente il passaggio 2, quando un utente tocca un punto attivo o una mappa immagine all&#39;interno del banner del carosello, tale interazione viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina web che contiene tutti i dati del punto attivo o della mappa immagine aggiunti in precedenza.

In un gestore eventi di questo tipo, il codice front-end esegue le seguenti operazioni:

* Ascolta un evento emesso dal banner del carosello.
* Costruisce un URL Quickview in base ai dati del punto attivo o della mappa immagine.
* Attiva il processo di caricamento di Quickview dal backend e di rendering sullo schermo per la visualizzazione.

Il codice di incorporamento restituito da Experience Manager Assets contiene già un gestore di eventi pronto all’uso ed è stato aggiunto un commento.

Pertanto, è necessario solo rimuovere il commento dal codice e sostituire il corpo del gestore fittizio con il codice specifico per la particolare pagina web.

Il processo di costruzione dell’URL Quickview è opposto a quello utilizzato per identificare le variabili hotspot e mappa immagine trattate in precedenza.

Consulta [Identificare le variabili hotspot e mappa immagine](#identifying-hotspot-and-image-map-variables).

L’ultimo passaggio per attivare l’URL Quickview e il pannello Quickview richiede probabilmente l’assistenza di un responsabile IT front-end del reparto IT. Possiedono le conoscenze necessarie per sapere come attivare con precisione l’implementazione Quickview dal passaggio corretto, avendo un URL Quickview pronto all’uso.

## Creare pop-up personalizzati utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

Vedi [Creare pop-up personalizzati utilizzando Quickview](/help/assets/custom-pop-ups.md).
