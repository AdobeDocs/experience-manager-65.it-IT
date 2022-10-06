---
title: Banner a carosello
description: Scopri come utilizzare i banner a carosello in Dynamic Media
uuid: 73684a08-d84d-4665-ab89-3a1bf88ac5dd
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e26c7f7f-bdd7-421a-8614-ba48abf381d2
docset: aem65
feature: Carousel Banners
role: User, Admin
exl-id: 53d34d3a-ecb6-4fa0-9665-60d21f48021e
source-git-commit: 5192a284c38eb10c214c67a8727de0f7dd4d1ee2
workflow-type: tm+mt
source-wordcount: '4730'
ht-degree: 2%

---

# Banner a carosello{#carousel-banners}

I banner a carosello consentono agli addetti al marketing di guidare la conversione creando facilmente contenuti promozionali interattivi rotanti e consegnandoli a qualsiasi schermo.

La creazione e la modifica dei contenuti contenuti contenuti nei banner promozionali può richiedere molto tempo, limitando la possibilità di pubblicare rapidamente nuovi contenuti o renderli più mirati. I banner a carosello consentono di creare o modificare rapidamente i banner rotanti. È possibile aggiungere interattività quali punti attivi che si collegano ai dettagli del prodotto o alle risorse correlate e consegnarli a qualsiasi schermo, consentendo di immettere nuovi contenuti promozionali sul mercato più rapidamente.

I banner a carosello sono contrassegnati da un banner con la parola **[!UICONTROL CAROUSELSET]**

![chlimage_1-438](assets/chlimage_1-438.png)

Sul sito web, un banner a carosello può essere visualizzato come segue:

![chlimage_1-439](assets/chlimage_1-439.png)

Qui puoi navigare tra le immagini (facendo clic sui numeri). Inoltre, le diapositive ruotano automaticamente in base a un intervallo di tempo personalizzabile. Le immagini aggiunte nei banner carosello supportano sia punti attivi che mappe immagine, in cui gli utenti possono selezionare o passare a un collegamento ipertestuale o accedere a una finestra Quickview.

In questo esempio, un utente ha toccato o fatto clic su una mappa immagine e ha effettuato l’accesso alla finestra Quickview per i guanti:

![chlimage_1-440](assets/chlimage_1-440.png)

## Guarda come vengono creati i banner a carosello {#watch-how-carousel-banners-are-created}

Esegui una procedura dettagliata su [creazione dei banner a carosello](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)(10 minuti e 33 secondi). Inoltre, viene illustrato come visualizzare in anteprima, modificare e distribuire banner a carosello.

>[!NOTE]
>
>Gli utenti non amministrativi devono essere aggiunti al **[!UICONTROL utenti dam]** per poter creare o modificare banner carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all’amministratore di sistema che può aggiungerti al **[!UICONTROL utenti dam]** gruppo.

## Avvio rapido: Banner a carosello {#quick-start-carousel-banners}

Per iniziare a usare rapidamente i banner a carosello:

1. [Identificare le variabili dei punti attivi e delle mappe immagine](#identifying-hotspot-and-image-map-variables) (solo per i clienti che utilizzano Experience Manager Assets + Dynamic Media)

   Per iniziare, identifica le variabili dinamiche utilizzate dall’implementazione Quickview esistente in modo da poter inserire correttamente i punti attivi e i dati della mappa immagine durante il processo di creazione del banner carosello in Adobe Experience Manager Assets.

   >[!NOTE]
   >
   >Se sei un cliente Experience Manager Sites o Ecommerce, puoi utilizzare la funzione integrata per passare alle pagine dei prodotti e cercare gli SKU esistenti (Stock Keeping Unit) nel catalogo dei prodotti. Non è necessario immettere manualmente le variabili punto attivo o mappa immagine. Consulta le informazioni su [configurazione di eCommerce](/help/commerce/cif-classic/administering/generic.md).
   >
   >
   >Se sei un cliente di Experience Manager Assets e Dynamic Media, inserisci manualmente i dati per gli hotspot e le mappe immagine, e quindi integra l’URL pubblicato o il codice da incorporare con il tuo sistema di gestione dei contenuti di terze parti.

1. Facoltativo: se necessario, [crea un predefinito visualizzatore per set carosello](/help/assets/managing-viewer-presets.md).

   Gli amministratori possono personalizzare il comportamento e l’aspetto del carosello creando un proprio predefinito per visualizzatori Carosello. Il vantaggio principale è che è possibile riutilizzare questo predefinito visualizzatore personalizzato per più caroselli. Tuttavia, se lo desideri, gli utenti possono personalizzare direttamente il comportamento e l’aspetto del carosello durante la creazione del carosello. Questo metodo è l’approccio preferito quando si desidera una progettazione specifica per un determinato carosello.

1. [Caricare un banner immagine](#uploading-image-banners).

   Carica i banner immagine che desideri rendere interattivi.

1. [Crea set carosello](#creating-carousel-sets).

   In Set caroselli, gli utenti navigano tra le immagini dei banner e selezionano punti attivi o mappe immagine per accedere ai contenuti pertinenti.

   Per creare un set carosello in Assets, seleziona **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL Set carosello]**. Aggiungi risorse alle diapositive e seleziona **[!UICONTROL Salva]**. Inoltre, puoi modificare l’aspetto e il comportamento del carosello direttamente nell’editor.

1. [Aggiungere punti attivi o mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).

   Aggiungi uno o più punti attivi o mappe immagine a un banner immagine e associali ciascuno di essi a un&#39;azione come un collegamento, una visualizzazione rapida o un frammento esperienza. Dopo aver aggiunto punti attivi o mappe immagine, finisci questa attività pubblicando il set carosello. La pubblicazione crea il codice di incorporamento che puoi utilizzare per copiare e applicare alla pagina di destinazione del tuo sito web.

   Vedi [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners) - Facoltativo. Se lo desideri, puoi visualizzare una rappresentazione del set carosello e verificarne l’interattività.

1. [Pubblicare banner a carosello](#publishing-carousel-banners).

   Puoi pubblicare un set carosello come faresti con una risorsa. In Assets, individua il set carosello, selezionalo e selezionalo **[!UICONTROL Pubblica]**. La pubblicazione di un set carosello attiva l’URL e la stringa di incorporamento.

1. Effettua una delle operazioni seguenti:

   * [Aggiungere un banner carosello alla pagina del sito web](#adding-a-carousel-banner-to-your-website-page) Puoi aggiungere l’URL del banner carosello o il codice di incorporamento copiato nella pagina del sito web.

      * [Integrare il banner carosello con una Quickview esistente](#integrating-the-carousel-banner-with-an-existing-quickview). Se utilizzi un sistema di gestione dei contenuti web di terze parti, devi integrare il nuovo banner carosello con l’implementazione Quickview esistente sul tuo sito web.
   * [Aggiungi un banner carosello al sito web in Experience Manager](/help/assets/adding-dynamic-media-assets-to-pages.md) Se sei un cliente Experience Manager Sites, puoi aggiungere il set carosello direttamente alla pagina nell’Experience Manager, utilizzando il componente File multimediali interattivi .


Per modificare i set carosello, vedi [modifica di set carosello](#editing-carousel-sets). Inoltre, puoi visualizzare e modificare [Proprietà del set carosello](manage-assets.md#editing-properties).

## Identificare le variabili dei punti attivi e delle mappe immagine {#identifying-hotspot-and-image-map-variables}

Per iniziare, identifica le variabili dinamiche utilizzate dall&#39;implementazione esistente di Quickview in modo da poter inserire correttamente i punti attivi o i dati della mappa immagine durante il processo di creazione del set carosello in Experience Manager Assets.

Quando aggiungi punti attivi o mappe immagine a un&#39;immagine del banner in Experience Manager Assets, assegna un SKU e variabili aggiuntive facoltative a ogni punto attivo o mappa immagine. Tali variabili vengono utilizzate in seguito per far corrispondere hotspot o mappe immagine con contenuto Quickview.

>[!NOTE]
>
>Se sei un cliente Experience Manager Sites e/o Experience Manager e-commerce, salta questo passaggio. Non è necessario identificare manualmente le variabili dei punti attivi o delle mappe immagine; puoi utilizzare l’integrazione con e-commerce per l’integrazione dei prodotti. Consulta le informazioni su [configurazione di eCommerce](/help/commerce/cif-classic/administering/generic.md). Inoltre, puoi utilizzare il componente interattivo e aggiungerlo alla pagina web.
>
>Se sei un cliente Experience Manager Assets o Media, pubblica l’URL o il codice da incorporare e poi ti integra con il tuo sistema di gestione dei contenuti di terze parti e individua manualmente gli hotspot e le mappe immagine.

È importante identificare in modo appropriato il numero e il tipo di variabili da associare ai dati del punto attivo o della mappa immagine. Ogni punto attivo o mappa immagine aggiunta a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo non ambiguo il prodotto nel sistema di back-end esistente. Allo stesso tempo, ogni punto attivo o mappa immagine non deve includere più dati del necessario. Questo perché renderebbe il processo di immissione dei dati eccessivamente complesso e la gestione continua dei punti attivi o delle mappe immagine più soggetta a errori.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati dei punti attivi o delle mappe immagine.

A volte è sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione di Quickview esistente. È probabile che sappiano qual è il set minimo di dati necessari per identificare Quickview nel sistema. Tuttavia, in genere è anche possibile analizzare semplicemente il comportamento esistente del codice front-end.

La maggior parte delle implementazioni di Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, toccando un **[!UICONTROL Quickview]** pulsante .
* Il sito web invia una richiesta Ajax al backend per caricare i dati o il contenuto della visualizzazione rapida, se necessario.
* I dati Quickview vengono tradotti nel contenuto in preparazione al rendering sulla pagina web.
* Infine, il codice front-end esegue il rendering visivo di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito web esistente in cui è implementata la funzione Quickview. Attiva la visualizzazione rapida e acquisisci l’URL Ajax inviato dalla pagina web per il caricamento dei dati o del contenuto della visualizzazione rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser web moderni dispongono di ispettori web che svolgono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser web che includono ispettori web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere F12 (Windows) o Comando-Opzione-I (Mac) per aprire il pannello Strumenti per sviluppatori, quindi selezionare la scheda Rete.
* In Firefox, è possibile attivare il plug-in Firebug premendo F12 (Windows) o Comando-Opzione-I (Mac) e utilizzando la relativa scheda Net, oppure è possibile utilizzare lo strumento integrato Inspector e la relativa scheda Rete.

Quando il monitoraggio della rete è attivato nel browser, attiva la visualizzazione rapida nella pagina.

Ora trova l&#39;URL Ajax Quickview nel registro di rete e copia l&#39;URL registrato per analisi future. Solitamente, quando si attiva la visualizzazione rapida sono presenti numerose richieste inviate al server. In genere, l’URL Ajax Quickview è uno dei primi dell’elenco. Dispone di una porzione o di un percorso di stringa di query complessa e il relativo tipo MIME di risposta è `text/html`, `text/xml`oppure `text/javascript`.

Durante questo processo, è importante visitare diverse aree del sito web, con diverse categorie di prodotti e tipi. Il motivo è che gli URL di visualizzazione rapida hanno parti comuni per una determinata categoria di siti web, ma cambiano solo se visiti un’area diversa del sito web.

Nel caso più semplice, l’unica parte variabile nell’URL Quickview è lo SKU del prodotto. In questo caso, il valore SKU è l’unico elemento dati necessario per aggiungere punti attivi o mappe immagine all’immagine del banner.

Tuttavia, in casi complessi, l’URL Quickview presenta diversi elementi diversi rispetto all’SKU, ad esempio ID categoria, codice colore e codice dimensione. In questi casi, ogni elemento è una variabile separata nella definizione dei dati del punto attivo o della mappa immagine nella funzione del banner carosello.

Prendi in considerazione i seguenti esempi di URL di visualizzazione rapida e le relative variabili di punti attivi o mappe immagine risultanti:

<table>
 <tbody>
  <tr>
   <td>SKU singolo, trovato nella stringa query.</td>
   <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L’unica parte variabile nell’URL è il valore della variabile <code>productId=</code> parametro della stringa query, ed è chiaramente un valore SKU. Pertanto, gli hotspot o le mappe immagine richiedono solo campi SKU popolati con valori come <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>SKU singolo, trovato nel percorso URL.</td>
   <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU delle hotspot/mappe immagine:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID categoria nella stringa query.</td>
   <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. La SKU viene memorizzata nel <code>prodId</code> e l'ID della categoria viene memorizzato nella variabile <code>category=</code>parametro .</p> <p>Di conseguenza, le definizioni dei punti attivi e delle mappe immagine sono coppie. Cioè, un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
     <li><p>SKU <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
     <li><p>SKU <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Carica banner immagine {#uploading-image-banners}

Se hai già caricato le immagini da utilizzare, passa al passaggio successivo, [Crea set carosello](#creating-carousel-sets). Le immagini utilizzate nel carosello devono essere caricate dopo l’abilitazione di Dynamic Media.

Per caricare i banner immagine, vedi [Caricare le risorse](/help/assets/manage-assets.md).

## Crea set carosello {#creating-carousel-sets}

>[!NOTE]
>
>Gli utenti non amministrativi devono essere aggiunti al **[!UICONTROL utenti dam]** per creare o modificare banner carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all’amministratore di sistema che può aggiungerti al **[!UICONTROL utenti dam]** gruppo.

**Per creare dei set carosello:**

1. In Assets, individua la cartella in cui vuoi creare il set carosello e vai a **[!UICONTROL Crea]** > **[!UICONTROL Set carosello]**.
1. Nella pagina dell’editor dei banner carosello, seleziona **[!UICONTROL Tocca per aprire il selettore risorse]** per selezionare l&#39;immagine per la prima diapositiva.

   Nella pagina dell’editor dei banner carosello, effettua una delle seguenti operazioni:

   * Nell’angolo in alto a sinistra della pagina, seleziona **[!UICONTROL Aggiungi diapositiva]** icona.

   * Vicino al centro della pagina, seleziona **[!UICONTROL Tocca per aprire il selettore risorse]**.
   Seleziona per selezionare le risorse da includere nel set carosello. Le risorse selezionate dispongono di un’icona a forma di segno di spunta. Al termine, seleziona **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando o facendo clic su **[!UICONTROL Invio]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e quindi seleziona la **[!UICONTROL Filtro]** sulla barra degli strumenti. Per modificare la visualizzazione, tocca l’icona Visualizza e fai clic su **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a elenco]**.

   Vedi [Utilizzare i selettori](/help/assets/working-with-selectors.md) per ulteriori informazioni.

1. Continua ad aggiungere diapositive finché non avrai aggiunto tutte le immagini da ruotare nel set carosello.
1. (Facoltativo) Effettua una delle seguenti operazioni:

   * Se necessario, trascinate le diapositive per riordinare le immagini nell’elenco del set.
   * Per eliminare un’immagine, selezionala e seleziona **[!UICONTROL Elimina diapositiva]** sulla barra degli strumenti.

   * Per applicare un predefinito, vicino all’angolo superiore destro della pagina, seleziona l’elenco a discesa dei predefiniti , quindi seleziona un predefinito da applicare al set contemporaneamente.
   Per eliminare una diapositiva, selezionarla e quindi selezionare la diapositiva sulla barra degli strumenti **[!UICONTROL Elimina diapositiva]**. Per spostare una diapositiva, selezionate l&#39;icona di riordino e tenete premuto e spostate nella posizione desiderata.

1. Dopo aver aggiunto le immagini nelle diapositive, puoi aggiungere un punto attivo, una mappa immagine o entrambi all’immagine. Vedi [Aggiungere punti attivi o mappe immagine a un banner immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
1. È possibile modificare la progettazione visiva e il comportamento dei set carosello. Seleziona la **[!UICONTROL Comportamento]** e **[!UICONTROL Aspetto]** e regola l’aspetto del banner carosello o il comportamento di componenti specifici. Vedi [Gestire i predefiniti per visualizzatori](/help/assets/viewer-presets.md) per ulteriori informazioni su come utilizzare l’editor per visualizzatori.

   >[!NOTE]
   >
   >Per i banner a carosello, puoi regolare quanto segue:
   >
   >    * Durata visualizzata da un’immagine. Per impostazione predefinita, ogni immagine viene visualizzata per 9 secondi.
   >    * Animazione. Per impostazione predefinita, ogni transizione di diapositiva è una dissolvenza. È possibile passare a una transizione diapositiva.
   >    * Stile dei pulsanti. Gli utenti possono ruotare attraverso i banner toccando ogni punto o numero. È possibile modificare la posizione in cui vengono visualizzati i pulsanti degli indicatori impostati (e se si tratta di uno stile numerico o punteggiato) e la loro dimensione.
   >    * Modifica lo stile di evidenziazione di una mappa immagine o dell’icona utilizzata per gli hotspot.
   >    * Prima di modificare un predefinito visualizzatore, scegli lo stile su cui desideri che sia basato il predefinito. Se non scegli uno stile, quando inizi a modificare il predefinito visualizzatore, perderai tutte le modifiche se decidi di cambiare un predefinito diverso.

   >
   >Vedi [Considerazioni speciali per i banner a carosello](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset) per istruzioni dettagliate e ulteriori informazioni sull’editor per visualizzatori.

   È inoltre possibile visualizzare in anteprima l’aspetto del banner carosello. Vedi [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners).

1. Seleziona **[!UICONTROL Salva]** una volta finito.

## Aggiunta di punti attivi o mappe immagine a un banner immagine {#adding-hotspots-or-image-maps-to-an-image-banner}

Puoi aggiungere punti attivi o mappe immagine a un banner utilizzando l’editor per set carosello.

Quando aggiungi punti attivi o mappe immagine, puoi definirli come una visualizzazione a comparsa Quickview, come un collegamento ipertestuale o un frammento esperienza.

Vedi [Frammento esperienza](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Gli strumenti di condivisione social media nel banner carosello non sono supportati quando incorpori il visualizzatore in un frammento esperienza.
>
>Per risolvere questo problema, puoi utilizzare o creare predefiniti visualizzatore privi di strumenti di condivisione social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.

Quando aggiungi punti attivi o mappe immagine a un&#39;immagine, ricorda di salvare il tuo lavoro. Le opzioni Annulla e Ripristina, situate nell’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione del banner carosello, puoi facoltativamente utilizzare Anteprima per visualizzare una rappresentazione dell’aspetto del banner carosello per i clienti.

Vedi [(Facoltativo) Anteprima banner carosello](#optional-previewing-carousel-banners).

>[!NOTE]
>
>Quando aggiungi punti attivi a un&#39;immagine in un [Immagine interattiva](/help/assets/interactive-images.md) Per un banner carosello, le informazioni relative al punto attivo vengono memorizzate nella stessa posizione dei metadati. Tale posizione è relativa alla posizione dell’immagine, indipendentemente dal fatto che si tratti di un’immagine interattiva o di un banner a carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai relativi dati definiti per i punti attivi, in entrambi i visualizzatori.
Tuttavia, i banner carosello supportano mappe immagine su immagini che possono contenere anche punti attivi; un&#39;immagine interattiva non lo è. Tieni presente questa regola se intendi creare un&#39;immagine interattiva o un banner carosello che utilizza la stessa immagine. Prendi in considerazione la creazione di immagini interattive e di banner a carosello utilizzando copie separate della stessa immagine.

>[!NOTE]
Se modifichi immagini interattive con punti attivi e ritagli l’immagine, questi vengono rimossi.

Vedi anche [Aggiungi mappe immagine](/help/assets/image-maps.md).

**Per aggiungere punti attivi o mappe immagine a un banner immagine:**

1. Da Risorse, accedi al set carosello che desideri rendere interattivo.
1. Seleziona il set carosello e fai clic su **[!UICONTROL Modifica]**. Viene aperto l’Editor visualizzatore carosello.
1. Selezionare la diapositiva da rendere interattiva.
1. Nell’angolo in alto a sinistra della pagina, seleziona **[!UICONTROL Punto attivo]** o **[!UICONTROL Mappa immagine]**.
1. Effettua una delle seguenti operazioni:

   * Per gli hotspot: Nell’immagine, seleziona la posizione in cui vuoi visualizzare il punto attivo.
   * Per le mappe immagine: Nell’immagine, seleziona , quindi trascina dall’alto a sinistra verso il basso a destra per creare l’area della mappa immagine. È possibile regolare le dimensioni della mappa immagine trascinando gli angoli.

   Se necessario, trascina il punto attivo o la mappa immagine in una nuova posizione. Aggiungi altri punti attivi o mappe immagine se necessario.

   Per eliminare un punto attivo o una mappa immagine, seleziona la **[!UICONTROL Azioni]** scheda . Seleziona il nome del punto attivo o della mappa immagine da rimuovere dall’intestazione **[!UICONTROL Mappe e punti attivi]** del menu a discesa **[!UICONTROL Tipo selezionato]**. Seleziona la **[!UICONTROL Cestino]** accanto al menu , quindi seleziona **[!UICONTROL Elimina]**.

1. Nel campo di testo Nome , digita il nome del punto attivo o della mappa immagine. Questo nome viene visualizzato anche nel **[!UICONTROL Mappe e punti attivi]** elenco a discesa. Se specifichi un nome, identifica facilmente il punto attivo o la mappa immagine se decidi di modificarlo in futuro.
1. Effettua una delle seguenti operazioni nel **[!UICONTROL Azioni]** scheda:

   * Seleziona **[!UICONTROL Quickview]**.

      * Se sei un cliente Experience Manager Sites ed e-commerce, seleziona l’icona Selettore prodotto (lente di ingrandimento) per aprire la pagina Seleziona prodotto . Seleziona il prodotto da utilizzare, quindi fai clic sul segno di spunta nell’angolo superiore destro della pagina per tornare all’editor dei banner carosello.
      * Se non sei un cliente Experience Manager Sites o Ecommerce

         * Vedi [Identificare le variabili dei punti di attivazione](#identifying-hotspot-and-image-map-variables) se desideri definire queste variabili.
         * Quindi, inserisci manualmente il valore SKU. Nel campo di testo Valore SKU digitare la SKU (Stock Keeping Unit) del prodotto, che è un identificatore univoco per ogni prodotto o servizio distinto offerto. Il valore SKU inserito popola automaticamente la parte variabile del modello Quickview in modo che il sistema sappia associare il punto attivo toccato a una particolare visualizzazione rapida SKU.
         * (Facoltativo) Se nella visualizzazione rapida sono presenti altre variabili da utilizzare per identificare ulteriormente un prodotto, seleziona **[!UICONTROL Aggiungi variabile generica]**. Nel campo di testo, specifica una variabile aggiuntiva. Ad esempio, category=Mens è una variabile aggiunta.

         * Vedi [Utilizzare i selettori](/help/assets/working-with-selectors.md) per ulteriori informazioni.
   * Seleziona **[!UICONTROL Collegamento ipertestuale]**.

      * Se sei un cliente Experience Manager Sites, seleziona l’icona Selettore sito (cartella) per passare a un URL.
         >[!NOTE]
         Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine Experience Manager Sites.

      * Se si è un cliente autonomo, nel campo di testo HREF specificare il percorso completo dell&#39;URL di una pagina Web collegata.

   Assicurati di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Vedi [Utilizzo dei selettori](/help/assets/working-with-selectors.md) per ulteriori informazioni.

   * Seleziona **[!UICONTROL Frammento esperienza]**.

      * Se sei un cliente Experience Manager Sites, seleziona l’icona Ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza . Seleziona il frammento esperienza da utilizzare, quindi seleziona **[!UICONTROL Seleziona]** nell’angolo in alto a destra della pagina per tornare alla pagina di gestione dei punti attivi.
Vedi [Frammenti esperienza](/help/sites-authoring/experience-fragments.md).

      * Specifica la larghezza e l’altezza del frammento esperienza così come viene visualizzato sul banner.

         >[!NOTE]
         Gli strumenti di condivisione social media nel banner carosello non sono supportati quando incorpori il visualizzatore in un frammento esperienza.
         Per risolvere questo problema, crea predefiniti visualizzatore che non dispongono di strumenti di condivisione social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   È inoltre possibile visualizzare in anteprima l’aspetto del banner carosello. Vedi [(Facoltativo) Anteprima dei banner a carosello](#optional-previewing-carousel-banners).

1. Seleziona **[!UICONTROL Salva]**.
1. Pubblica il set carosello. La pubblicazione crea il codice di incorporamento o l’URL che puoi utilizzare sulla pagina del tuo sito web. Se sei un cliente Experience Manager Sites, puoi aggiungere il set carosello direttamente alla tua pagina web.

   Vedi [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md).

   Vedi [Aggiunta di un set carosello alla pagina di destinazione del sito web](#adding-a-carousel-banner-to-your-website-page)

## Modifica set carosello {#editing-carousel-sets}

>[!NOTE]
Gli utenti non amministrativi devono essere aggiunti al **[!UICONTROL utenti dam]** per poter creare o modificare banner carosello. In caso di problemi durante la creazione o la modifica, rivolgiti all’amministratore di sistema che può aggiungerti al **[!UICONTROL utenti dam]** gruppo.

È possibile eseguire varie attività di modifica sui set carosello, ad esempio:

* Aggiungi le diapositive a un set carosello. Vedi anche [Utilizzare i selettori](/help/assets/working-with-selectors.md).
* Riordinare le diapositive nel set carosello.
* Elimina le risorse nel set carosello.
* Applica un predefinito visualizzatore.
* Elimina il set carosello.
* Aggiungi o modifica punti attivi e mappe immagine. Vedi anche [Utilizzare i selettori](/help/assets/working-with-selectors.md).

**Per modificare i set carosello:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa Set carosello, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita).
   * Passa il puntatore del mouse su una risorsa Set carosello, seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi seleziona **[!UICONTROL Modifica]** sulla barra degli strumenti.

   * Seleziona una risorsa Set carosello, quindi nell’angolo in alto a sinistra della pagina seleziona **[!UICONTROL Modifica]** (icona a forma di matita).

1. Per modificare il set carosello, effettuate una delle seguenti operazioni:

   * Per aggiungere una diapositiva, seleziona la **[!UICONTROL Aggiungi diapositiva]** , quindi individua la risorsa da aggiungere alla diapositiva e seleziona il segno di spunta.
   * Per riordinare le diapositive, trascinate una diapositiva in una nuova posizione (selezionate l&#39;icona di riordino per spostare gli elementi).
   * Per aggiungere un punto attivo o una mappa immagine, seleziona le icone del punto attivo o della mappa immagine e vedi [aggiunta di punti attivi e mappe immagine](#adding-hotspots-or-image-maps-to-an-image-banner).
   * Per modificare l’aspetto o il comportamento del set carosello, seleziona la **[!UICONTROL Aspetto]** scheda o **[!UICONTROL Comportamento]** , quindi imposta le opzioni desiderate.
   * Per modificare punti attivi o mappe immagine, nella diapositiva appropriata seleziona un punto attivo o una mappa immagine e cambia come necessario in **[!UICONTROL Azioni]** scheda .
   * Per eliminare una diapositiva, selezionala, quindi seleziona **[!UICONTROL Elimina diapositiva]** sulla barra degli strumenti.
   * Per applicare un predefinito, seleziona la **[!UICONTROL Predefinito]** dall’elenco a discesa, quindi seleziona un predefinito visualizzatore.
   * Per eliminare un intero set carosello, passare al set carosello, selezionarlo, quindi selezionare **[!UICONTROL Elimina]**.

   >[!NOTE]
   Se modifichi immagini interattive con punti attivi e ritagli l’immagine, questi vengono rimossi.

## (Facoltativo) Anteprima banner carosello {#optional-previewing-carousel-banners}

Puoi utilizzare Anteprima per vedere come viene visualizzato il banner carosello ai clienti e per testare gli hotspot e le mappe immagine dei banner carosello per assicurarti che si comportino come previsto.

Quando sei soddisfatto del banner carosello, puoi pubblicarlo.
Vedi [Incorporamento del visualizzatore di video o immagini in una pagina web](/help/assets/embed-code.md).
Vedi [Collegamento di URL all’applicazione web](/help/assets/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine Experience Manager Sites.
Vedi [Aggiunta di risorse Dynamic Media alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).

Puoi visualizzare in anteprima i banner carosello dall’Editor carosello (metodo preferito) o dal **[!UICONTROL Visualizzatori]** elenco.

**Per visualizzare in anteprima i banner carosello:**

1. In **[!UICONTROL Risorse]**, passa a un banner carosello esistente creato e seleziona per aprirlo.
1. Seleziona **[!UICONTROL Modifica]**.
1. Nell’elenco dei predefiniti visualizzatore nell’angolo a destra della barra degli strumenti, seleziona un visualizzatore per visualizzare l’anteprima del banner carosello.

   ![experience_fragment-carouselbanner-riquadro a discesa](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Seleziona **[!UICONTROL Anteprima]**.
1. Seleziona gli hotspot o le mappe immagine sull&#39;immagine in modo da poterne testare le azioni associate.

**Per visualizzare in anteprima i banner a carosello dall’elenco Visualizzatori:**

1. In **[!UICONTROL Risorse]**, passa a un banner carosello esistente creato e seleziona per aprirlo.
1. Nell’angolo in alto a sinistra della pagina Anteprima, seleziona l’icona Contenuto .
1. In **[!UICONTROL Visualizzatori]** nel pannello a sinistra della pagina, seleziona il nome del predefinito visualizzatore del carosello banner da usare.
1. Seleziona gli hotspot o le mappe immagine sull&#39;immagine in modo da poterne testare le azioni associate.

## Pubblicare banner a carosello {#publishing-carousel-banners}

Pubblica il carosello in modo da poterlo utilizzare. La pubblicazione di un set carosello attiva l’URL e il codice di incorporamento. Pubblica anche il carosello su Dynamic Media cloud, integrato con una rete CDN per una distribuzione scalabile e performante.

>[!NOTE]
Se utilizzi un’immagine interattiva esistente con punti attivi per il banner carosello, devi pubblicare separatamente l’immagine interattiva dopo aver pubblicato il banner carosello.
Inoltre, se modifichi un’immagine interattiva pubblicata precedentemente che utilizzi in un banner carosello, devi pubblicare l’immagine interattiva prima che tali modifiche si riflettano nel banner carosello.

Vedi [Pubblicare risorse Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md) per informazioni su come pubblicare banner carosello.

## Aggiungere un banner carosello alla pagina del sito web {#adding-a-carousel-banner-to-your-website-page}

Dopo aver caricato le immagini del banner per creare un carosello, aggiunto gli hotspot e/o le mappe immagine al banner e pubblicato il set carosello, ora puoi aggiungerlo alla pagina del sito web esistente.

>[!NOTE]
Se sei un cliente di Experience Manager Sites, puoi aggiungere il banner carosello direttamente alla pagina trascinando il componente File multimediali interattivi nella pagina. Vedi [Aggiungere risorse Dynamic Media alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).

Tuttavia, se sei un cliente di risorse di Experience Manager autonome, puoi aggiungere manualmente il banner carosello alla pagina di destinazione del sito web come descritto in questa sezione.

1. Copia il codice di incorporamento del set carosello pubblicato.
Vedi [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/embed-code.md).

1. Aggiungi il codice di incorporamento copiato da Experience Manager Assets alla pagina web.
Il codice di incorporamento copiato è reattivo e deve quindi adattarsi automaticamente all’area di incorporamento della pagina.

## Integrare il banner carosello con una Quickview esistente {#integrating-the-carousel-banner-with-an-existing-quickview}

>[!NOTE]
Questo passaggio si applica solo se sei un cliente Experience Manager Assets autonomo.

L’ultimo passaggio di questo processo consiste nell’integrare il banner carosello con un’implementazione Quickview esistente sul sito web. Ogni implementazione di Quickview è unica ed è necessario un approccio specifico che implichi l&#39;assistenza di un utente IT front-end.

L&#39;implementazione di Quickview esistente rappresenta normalmente una catena di azioni correlate che avvengono sulla pagina web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito web.
1. Il codice front-end ottiene un URL Quickview basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto al passaggio 2.
1. La logica di back-end restituisce i dati o il contenuto Quickview corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto di Quickview.
1. Facoltativamente, il codice front-end converte i dati Quickview caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l’utente finale.

Queste chiamate non rappresentano chiamate API pubbliche indipendenti che possono essere richiamate dalla logica della pagina web da un passaggio arbitrario. Si tratta invece di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Contemporaneamente alla sostituzione del passaggio 1 e in parte del passaggio 2 da parte del banner carosello, quando un utente tocca un punto attivo o una mappa immagine all’interno del banner carosello, tale interazione viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina web che contiene tutti i dati del punto attivo o della mappa immagine precedentemente aggiunti.

In un tale gestore di eventi, il codice front-end effettua le seguenti operazioni:

* Ascolta un evento emesso dal banner carosello.
* Crea un URL di visualizzazione rapida basato sui dati del punto attivo o della mappa immagine.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering sullo schermo per la visualizzazione.

Il codice di incorporamento restituito da Experience Manager Assets dispone già di un gestore eventi ready-to-use in posizione, che viene aggiunto un commento.

Pertanto, è solo necessario rimuovere il commento dal codice e sostituire il corpo del gestore fittizio con il codice specifico per la pagina web specifica.

Il processo di costruzione dell’URL di visualizzazione rapida è opposto al processo utilizzato per identificare le variabili dei punti attivi e delle mappe immagine descritte in precedenza.

Vedi [Identificare le variabili dei punti attivi e delle mappe immagine](#identifying-hotspot-and-image-map-variables).

L&#39;ultimo passaggio per attivare l&#39;URL Quickview e attivare il pannello Quickview richiede molto probabilmente l&#39;assistenza di un esperto IT front-end del reparto IT. Hanno la conoscenza di sapere come attivare con precisione l&#39;implementazione di Quickview dal passaggio appropriato, avendo un URL di Quickview pronto all&#39;uso.

## Creare pop-up personalizzati utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

Vedi [Creare pop-up personalizzati utilizzando Quickview](/help/assets/custom-pop-ups.md).
