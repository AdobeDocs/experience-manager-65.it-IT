---
title: Operazioni di base quando si utilizza l’ambiente di authoring AEM
description: Acquisisci dimestichezza con AEM e il suo utilizzo di base
uuid: c78ef9da-e0bd-47be-a410-9cf2ae71749a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 21181a6f-b434-40ed-8eb1-ebdfc98964dd
docset: aem65
exl-id: ef1a3997-feb4-4cb0-9396-c8335b69bb10
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3017'
ht-degree: 64%

---

# Operazioni di base{#basic-handling}

>[!NOTE]
>
>* Questa pagina offre una panoramica delle operazioni di base nell’ambiente di authoring AEM. Usa la console **Sites** come base.
>
>* Alcune funzionalità non sono disponibili in tutte le console e in alcune console potrebbero essere disponibili funzionalità aggiuntive. Informazioni specifiche sulle singole console e sulle relative funzionalità saranno descritte più dettagliatamente in altre pagine.
>* AEM supporta l’utilizzo di scelte rapide da tastiera in numerose aree, in particolare per l’[utilizzo delle console](/help/sites-authoring/keyboard-shortcuts.md) e la [modifica delle pagine](/help/sites-authoring/page-authoring-keyboard-shortcuts.md).
>

## Guida introduttiva {#getting-started}

### Interfaccia touch {#a-touch-enabled-ui}

L’interfaccia utente AEM è stata abilitata per il tocco. L&#39;interfaccia touch consente di interagire con il software tramite gesti quali toccare, tenere premuto e scorrere. Questo è in contrasto con il funzionamento di un&#39;interfaccia desktop tradizionale con azioni del mouse come clic, doppio clic, clic con il pulsante destro del mouse e passaggio del mouse.

Poiché l’interfaccia utente dell’AEM è dotata di funzionalità touch, puoi utilizzare i gesti touch sui dispositivi touch (ad esempio, dispositivi mobili o tablet) e le azioni del mouse su un dispositivo desktop tradizionale.

### Primi passi {#first-steps}

Immediatamente dopo aver effettuato l’accesso, si aprirà il pannello di [navigazione](#navigation-panel). Selezionando una delle opzioni, si apre la rispettiva console.

![Navigazione](assets/bh-01.png)

>[!NOTE]
>
>Per illustrare l’utilizzo di base di AEM, in questo documento viene utilizzata la console **Sites.**
>
>Tocca o fai clic su **Sites** per iniziare.

### Navigazione nel prodotto  {#product-navigation}

Ogni volta che un utente accede per la prima volta a una console, viene avviato un tutorial relativo alla navigazione nel prodotto. Dedica alcuni minuti a seguire il tutorial per ottenere una buona panoramica dell’utilizzo di base di AEM.

![Navigazione nel prodotto ](assets/bh-02.png)

Tocca o fai clic su **Avanti** per passare alla pagina successiva della panoramica. Tocca o fai clic su **Chiudi** oppure tocca o fai clic all’esterno della finestra di dialogo della panoramica per chiuderla.

Se non visualizzi tutte le diapositive o non selezioni l’opzione, al prossimo accesso a una console la panoramica verrà riavviata **Non mostrare più**.

## Navigazione globale {#global-navigation}

Puoi spostarti tra le diverse console utilizzando il pannello di navigazione globale. Viene attivato come menu a discesa a schermo intero quando tocchi o fai clic sul collegamento Adobe Experience Manager in alto a sinistra dello schermo.

Per chiudere il pannello di navigazione globale e tornare alla posizione precedente, tocca o fai clic su **Chiudi**.

![Navigazione globale](assets/bh-03.png)

>[!NOTE]
>
>La prima volta che accedi presentavi il **Navigazione** pannello.

La navigazione globale presenta due pannelli, rappresentati da icone sul lato sinistro dello schermo:

* **[Navigazione](/help/sites-authoring/basic-handling.md#navigation-panel)**: rappresentata da una bussola 
* **[Strumenti](/help/sites-authoring/basic-handling.md#tools-panel)**: rappresentati da un martello

Le opzioni disponibili in questi pannelli sono descritte di seguito.

### Pannello di navigazione  {#navigation-panel}

Il pannello di navigazione consente di accedere alle console AEM:

![Navigazione](assets/bh-01.png)

Il titolo della scheda del browser si aggiorna per riflettere la posizione in cui ci si sposta nelle console e nel contenuto.

Nel pannello di navigazione sono disponibili le console seguenti:

<table>
 <tbody>
  <tr>
   <td><strong>Console</strong></td>
   <td><strong>Scopo</strong></td>
  </tr>
  <tr>
   <td>Assets<br /> </td>
   <td>Queste console consentono di importare e <a href="/help/assets/home.md">gestire le risorse digitali</a> ad esempio immagini, video, documenti e file audio. Queste risorse possono quindi essere utilizzate da qualsiasi sito web in esecuzione sulla stessa istanza AEM. </td>
  </tr>
  <tr>
   <td>Communities</td>
   <td>Questa console consente di creare e gestire <a href="/help/communities/sites-console.md">siti community</a> per <a href="/help/communities/overview.md#engagement-community">coinvolgimento</a> e <a href="/help/communities/overview.md#enablement-community">abilitazione</a>.</td>
  </tr>
  <tr>
   <td>Commerce</td>
   <td>Questo consente di gestire prodotti, cataloghi di prodotti e ordini relativi al <a href="/help/commerce/cif-classic/administering/ecommerce.md">Commerce</a> siti.</td>
  </tr>
  <tr>
   <td>Frammenti di esperienza</td>
   <td>Un <a href="/help/sites-authoring/experience-fragments.md">frammento esperienza</a> è un’esperienza autonoma che può essere riutilizzata su tutti i canali, supporta le varianti e non richiede di copiare e incollare le esperienze o parti di esse.</td>
  </tr>
  <tr>
   <td>Forms</td>
   <td>Questa console consente di creare, gestire ed elaborare le <a href="/help/forms/home.md">moduli e documenti</a>.</td>
  </tr>
  <tr>
   <td>Personalizzazione</td>
   <td>Questa console fornisce <a href="/help/sites-authoring/personalization.md">framework di strumenti per la creazione di contenuti mirati e la presentazione di esperienze personalizzate</a>.</td>
  </tr>
  <tr>
   <td>Progetti</td>
   <td>Il <a href="/help/sites-authoring/touch-ui-managing-projects.md">La console Progetti consente di accedere direttamente ai progetti</a>. I progetti sono dashboard virtuali. Possono essere utilizzati per creare un team, quindi fornire al team l’accesso a risorse, flussi di lavoro e attività, consentendo alle persone di lavorare su un obiettivo comune. <br /> </td>
  </tr>
  <tr>
   <td>Screens</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/authoring/setting-up-projects/creating-a-screens-project.html">Schermi</a> consente di gestire tutti gli schermi, di qualsiasi dimensione, che verranno visualizzati dai clienti ovunque si trovino.</td>
  </tr>
  <tr>
   <td>Sites</td>
   <td>Le console Sites consentono di: <a href="/help/sites-authoring/page-authoring.md">creare, visualizzare e gestire siti Web</a> in esecuzione sull’istanza AEM. Tramite queste console puoi creare, modificare, copiare, spostare ed eliminare pagine web, avviare flussi di lavoro e pubblicare pagine.<br /> </td>
  </tr>
 </tbody>
</table>

### Pannello Strumenti {#tools-panel}

Nel pannello Strumenti, ogni opzione nel pannello laterale contiene una serie di sottomenu. Il [Console Strumenti](/help/sites-administering/tools-consoles.md) qui puoi accedere a console e strumenti specifici per la gestione dei siti web, delle risorse digitali e di altri aspetti dell’archivio dei contenuti.

![Pannello Strumenti](assets/bh-04.png)

## Intestazione {#the-header}

L’intestazione di è sempre presente nella parte superiore dello schermo. Anche se la maggior parte delle opzioni presenti nell’intestazione rimangono invariate ovunque ti trovi nel sistema, alcune dipendono dal contesto.

![Intestazione](assets/bh-03.png)

* [Navigazione globale](#navigatingconsolesandtools)

  Seleziona il collegamento **Adobe Experience Manager** per spostarti tra le diverse console.

  ![il collegamento Adobe Experience Manager](assets/screen_shot_2018-03-23at103615.png)

* [Ricerca](/help/sites-authoring/search.md)

  ![Ricerca](do-not-localize/screen_shot_2018-03-23at103542.png)

  È anche possibile utilizzare il [tasto di scelta rapida](/help/sites-authoring/keyboard-shortcuts.md) `/` (barra obliqua) per richiamare la ricerca da qualsiasi console.

* [Soluzioni](https://www.adobe.com/it/experience-cloud.html)

  ![Soluzioni](do-not-localize/screen_shot_2018-03-23at103552.png)

* [Aiuto](#accessinghelptouchoptimizedui)

  ![Aiuto](do-not-localize/screen_shot_2018-03-23at103547.png)

* [Notifiche](/help/sites-authoring/inbox.md)

  ![Notifiche](do-not-localize/screen_shot_2018-03-23at103558.png)

  Questa icona viene contrassegnata con il numero di notifiche incomplete attualmente assegnate.

  >[!NOTE]
  >
  >L’AEM preconfigurato viene precaricato con le attività amministrative assegnate al gruppo di utenti amministratori. Consulta [Casella in entrata - Attività amministrative predefinite](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks) per i dettagli.

* [Proprietà utente](/help/sites-authoring/user-properties.md)

  ![Proprietà utente](do-not-localize/screen_shot_2018-03-23at103603.png)

* [Selettore della barra](/help/sites-authoring/basic-handling.md#rail-selector)

  ![L’elenco dei selettori della barra è visualizzato sul lato sinistro della schermata Adobe Experience Manager.](do-not-localize/screen_shot_2018-03-23at103943.png)

  Le opzioni visualizzate dipendono dalla console corrente. Ad esempio, in **Sites** puoi selezionare solo il contenuto (opzione predefinita), la timeline, i riferimenti o il pannello laterale del filtro.

  ![Selettore della barra](assets/screen_shot_2018-03-23at104029.png)

* Breadcrumb

  ![Breadcrumb](assets/bh-05.png)

  Situate al centro della barra, le breadcrumb mostrano sempre la descrizione dell’elemento attualmente selezionato e consentono di spostarsi all’interno di una console specifica. Nella console Sites puoi spostarti tra i vari livelli del sito web.

  Ti basterà fare clic sul testo della breadcrumb per visualizzare un elenco a discesa con i livelli della gerarchia dell’elemento selezionato. Fai clic su una voce per passare a quella posizione.

  ![Livelli gerarchici](assets/bh-06.png)

* Selezione del periodo di tempo di Analytics

  ![Periodo di tempo di Analytics](assets/screen_shot_2018-03-23at104126.png)

  È disponibile solo nella vista a elenco. Consulta [vista a elenco](#list-view) per ulteriori informazioni.

* Pulsante **Crea**

  ![Crea](assets/screen_shot_2018-03-23at104301.png)

  Dopo che hai fatto clic, le opzioni visualizzate sono adatte alla console/al contesto.

* [Viste](/help/sites-authoring/basic-handling.md#viewingandselectingyourresourcescardlistcolumn)

  L’icona di visualizzazione si trova all’estrema destra della barra degli strumenti di AEM. Inoltre, indica la vista corrente e ne consente la modifica. Ad esempio, la visualizzazione predefinita **Vista a colonne** presenta questa icona:

  ![Vista a colonne](assets/bh-07.png)

  È possibile passare dalla vista a colonne, alla vista a schede e alla vista a elenco e nella vista a elenco sono visualizzate anche le impostazioni di visualizzazione.

  ![Cambia visualizzazione](assets/bh-09.png)

* Navigazione tramite tastiera

  Potete navigare in un sito web utilizzando solo la tastiera. Questa utilizza la funzionalità standard del browser del **SCHEDA** chiave (o **OPZ+TAB**) per spostarti tra gli elementi della pagina che sono *focalizzabile*.

  Nella console di **Sites** è stata aggiunta l’opzione per **passare al contenuto principale**. Questo diventa visibile quando *scheda* tramite le opzioni di intestazione, e velocizza la navigazione consentendo di saltare gli elementi standard nella barra degli strumenti (prodotto) e di passare direttamente al contenuto principale.

  ![Passa al contenuto principale](assets/bh-30.png)

## Accedere all’Aiuto   {#accessing-help}

Sono disponibili diverse risorse di Aiuto:

* **Barra degli strumenti della console**

  A seconda della tua posizione, l’icona **Aiuto** consente di accedere alle risorse appropriate:

  ![Barra degli strumenti della console](assets/bh-10.png)

* **Navigazione**

  La prima volta che accedi al sistema, compare [una serie di diapositive introduttive su come navigare in AEM](/help/sites-authoring/basic-handling.md#product-navigation).

* **Editor pagina**

  La prima volta che modifichi una pagina, compare una serie di diapositive introduttive sull’editor pagina.

  ![Editor pagina](assets/bh-11.png)

  Esamina questa panoramica come faresti con la [panoramica di navigazione del prodotto](/help/sites-authoring/basic-handling.md#product-navigation) la prima volta che accedi a una console.

  Dal menu [**Informazioni sulle pagine** puoi selezionare **Aiuto**](/help/sites-authoring/author-environment-tools.md#accessing-help) per accedervi di nuovo in un secondo tempo.

* **Console Strumenti**

  Dalla console **Strumenti** è possibile inoltre accedere alle **Risorse** esterne:

   * **Documentazione**
Consulta la documentazione su Web Experience Management.

   * **Risorse per sviluppatori**
Risorse per sviluppatori e download

  >[!NOTE]
  >
  >Puoi accedere in qualsiasi momento ai tasti di scelta rapida, semplicemente utilizzando il tasto di scelta rapida `?` (punto interrogativo) all’interno della console.
  >
  >Per una panoramica di tutte le scelte rapide da tastiera, consulta la documentazione seguente:
  >
  >* [Scelte rapide da tastiera per la modifica delle pagine](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
  >* [Scelte rapide da tastiera per le console](/help/sites-authoring/keyboard-shortcuts.md)

## Barra delle azioni  {#actions-toolbar}

Ogni volta che viene selezionata una risorsa (ad esempio una pagina o una risorsa), le icone indicano diverse azioni, con testo descrittivo nella barra degli strumenti. Queste azioni dipendono da:

* La console corrente.
* Il contesto attuale.
* Se sei o meno in modalità [Selezione](#navigatingandselectionmode).

L’azione disponibile nella barra degli strumenti varia per riflettere le azioni che puoi eseguire sugli oggetti specifici selezionati.

La modalità di [selezione di una risorsa](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) dipende dalla vista.

A causa del poco spazio disponibile in alcune finestre, la barra può facilmente superare lo spazio a disposizione. In questo caso compaiono altre opzioni. Tocca o fai clic sui tre puntini (**...**) per aprire un selettore a discesa contenente tutte le azioni che non rientrano nella barra. Ad esempio, dopo la selezione di una pagina nella console **Sites**:

![Barra delle azioni ](assets/bh-12.png)

>[!NOTE]
>
>Le singole icone disponibili sono documentate in relazione alla console, alla funzione o allo scenario appropriato.

## Azioni rapide  {#quick-actions}

In entrata [Vista a schede](#cardviewquickactions) alcune azioni sono disponibili come icone di azione rapida e sono disponibili nella barra degli strumenti. Le icone delle azioni rapide sono disponibili per un singolo elemento alla volta ed evitano di dover preselezionare le opzioni.

La azioni rapide sono visibili con un tocco prolungato (su dispositivo touch) sulla scheda di una risorsa. Le azioni rapide disponibili possono dipendere dalla console e dal contesto. Ad esempio, di seguito sono riportate le azioni rapide per una pagina nella console **Sites**:

![Azioni rapide](assets/bh-13.png)

## Visualizzazione e selezione delle risorse {#viewing-and-selecting-resources}

In tutte le viste la visualizzazione, la navigazione e la selezione funzionano allo stesso modo, ma con lievi variazioni a seconda della vista attiva.

Puoi visualizzare, navigare e selezionare (per ulteriori azioni) le risorse in una qualsiasi delle viste disponibili, selezionabili dall’icona in alto a destra:

* [Vista a colonne](#column-view)
* [Vista a schede](#card-view)

* [Vista a elenco ](#list-view)

>[!NOTE]
>
>Per impostazione predefinita, AEM Assets non visualizza le rappresentazioni originali delle risorse nell’interfaccia utente come miniature in nessuna delle viste. Se sei un amministratore, puoi utilizzare le sovrapposizioni per configurare AEM Assets in modo da visualizzare le rappresentazioni originali come miniature.

### Selezionare le risorse  {#selecting-resources}

La selezione di una specifica risorsa dipende dalla combinazione della vista e del dispositivo utilizzati:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td>Seleziona</td>
   <td>Deseleziona</td>
  </tr>
  <tr>
   <td>Vista a colonne<br /> </td>
   <td>
    <ul>
     <li>Desktop:<br /> Fai clic sulla miniatura</li>
     <li>Dispositivo mobile:<br /> Tocca la miniatura</li>
    </ul> </td>
   <td>
    <ul>
     <li>Desktop:<br /> Fai clic sulla miniatura</li>
     <li>Dispositivo mobile:<br /> Tocca la miniatura</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Vista a schede<br /> </td>
   <td>
    <ul>
     <li>Desktop:<br /> Passa il puntatore del mouse, quindi utilizza l’azione rapida con segno di spunta</li>
     <li>Dispositivo mobile:<br /> Tocca e tieni premuto sulla scheda</li>
    </ul> </td>
   <td>
    <ul>
     <li>Desktop:<br /> Fai clic sulla scheda</li>
     <li>Dispositivo mobile:<br /> Tocca la scheda</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Vista a elenco </td>
   <td>
    <ul>
     <li>Desktop:<br /> Fai clic sulla miniatura</li>
     <li>Dispositivo mobile:<br /> Tocca la miniatura</li>
    </ul> </td>
   <td>
    <ul>
     <li>Desktop:<br /> Fai clic sulla miniatura</li>
     <li>Dispositivo mobile:<br /> Tocca la miniatura</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Seleziona tutto {#select-all}

Per selezionare tutti gli elementi in qualsiasi vista, fai clic sull’opzione **Seleziona tutto** nell’angolo in alto a destra della console.

* Nella **Vista a schede**, vengono selezionate tutte le schede.
* In entrata **Vista a elenco** vengono selezionati tutti gli elementi dell’elenco.
* Nella **Vista a colonne**, vengono selezionati tutti gli elementi nella colonna più a sinistra.

![Seleziona tutto](assets/screen-shot_2019-03-05at094659.png)

#### Deselezionare tutti gli elementi {#deselecting-all}

In tutti i casi in cui selezioni elementi, il numero degli elementi selezionati viene visualizzato in alto a destra nella barra degli strumenti.

Per deselezionare tutti gli elementi e uscire dalla modalità di selezione, effettuare le seguenti operazioni:

* tocca o fai clic sul pulsante **X** accanto al conteggio,

* o utilizzando **escape**.

![Deseleziona](assets/bh-14.png)

In tutte le viste, tutti gli elementi possono essere deselezionati toccando escape sulla tastiera se si utilizza un dispositivo desktop.

#### Esempio di selezione {#selecting-example}

1. Ad esempio, nella vista a schede:

   ![Seleziona - Vista a schede](assets/bh-15.png)

1. Dopo la selezione di una risorsa, l’intestazione superiore è coperta dalla [barra delle azioni](#actionstoolbar), che permette di accedere alle azioni applicabili alla risorsa selezionata.

   Per uscire dalla modalità di selezione, seleziona la **X** in alto a destra oppure premi **Esc**.

### Vista a colonne {#column-view}

![Vista a colonne](assets/bh-16.png)

La vista a colonne consente la navigazione visiva di una struttura di contenuti tramite una serie di colonne in cascata. Questa visualizzazione consente di visualizzare e scorrere la struttura ad albero del sito web.

Quando si seleziona una risorsa nella prima colonna a sinistra, vengono visualizzate le risorse secondarie in una colonna a destra. Quando si seleziona una risorsa nella colonna a destra, vengono visualizzate le risorse secondarie in un’altra colonna a destra, e così via.

* Per spostarti verso l’alto o il basso nella struttura ad albero, tocca o fai clic sul nome della risorsa o sulla freccia a destra del nome.

   * Il nome della risorsa e la freccia vengono evidenziati quando tocca o fai clic su di essa.

     ![Vista a colonne](assets/bh-17.png)

   * Gli elementi secondari della risorsa che hai toccato o su cui hai fatto clic vengono visualizzati nella colonna a destra di tale risorsa.
   * Se tocchi o fai clic su un nome di risorsa senza elementi secondari, i relativi dettagli verranno visualizzati nella colonna finale.

* Quando tocchi o fai clic sulla miniatura, la risorsa viene selezionata.

   * Quando questa opzione è selezionata, sulla miniatura compare un segno di spunta e viene evidenziato anche il nome della risorsa.
   * I dettagli della risorsa selezionata sono visualizzati nella colonna finale.
   * La barra degli strumenti delle azioni diventa disponibile.

     ![Vista a colonne](assets/bh-18.png)

  Quando una pagina viene selezionata nella vista a colonne, viene visualizzata nella colonna finale con i seguenti dettagli:

   * Titolo pagina
   * Nome pagina (parte dell’URL della pagina)
   * Modello su cui si basa la pagina
   * Dettagli di modifica
   * Lingua della pagina
   * Dettagli pubblicazione

### Vista a schede {#card-view}

![bh-15-1](assets/bh-15-1.png)

* La vista a schede mostra le schede informative per ogni elemento al livello corrente, che forniscono informazioni quali:

   * Una rappresentazione visiva del contenuto della pagina.
   * Il titolo della pagina.
   * Date importanti (ad esempio ultima modifica, ultima pubblicazione).
   * Se la pagina è bloccata, nascosta o fa parte di una Live Copy.
   * Se appropriato, quando devi eseguire un’azione nell’ambito di un flusso di lavoro.

      * Alle voci della [Casella in entrata](/help/sites-authoring/inbox.md) possono essere correlati dei marcatori che indicano le azioni necessarie.

* In questa vista sono disponibili anche [azioni rapide](#quick-actions), per effettuare selezioni ed eseguire le operazioni più comuni, come la modifica.

  ![Vista a schede - Azioni rapide](assets/bh-13-1.png)

* Per spostarti verso il basso nella struttura, tocca o fai clic sulle schede (facendo attenzione a evitare le azioni rapide); per tornare verso l’alto utilizza le [breadcrumb nell’intestazione](/help/sites-authoring/basic-handling.md#the-header).

### Vista a elenco  {#list-view}

![Vista a elenco](assets/bh-19.png)

* Nella vista a elenco sono elencate le informazioni di ogni risorsa al livello corrente.
* Per spostarti verso il basso nella struttura, tocca o fai clic sul nome delle risorse; per tornare verso l’alto utilizza le [breadcrumb nell’intestazione](/help/sites-authoring/basic-handling.md#the-header).

* Per selezionare tutti gli elementi nell’elenco, utilizza la casella di selezione in alto a sinistra nell’elenco.

  ![Vista a elenco - Seleziona tutto](assets/bh-20.png)

   * Quando tutti gli elementi dell’elenco sono selezionati, viene selezionata la casella di controllo.

      * Tocca o fai clic sulla casella di controllo per deselezionare tutti gli elementi.

   * Se sono selezionati solo alcuni elementi, viene visualizzato un segno meno.

      * Tocca o fai clic sulla casella di controllo per selezionare tutti gli elementi.
      * Tocca o fai di nuovo clic sulla casella di controllo per deselezionare tutti gli elementi.

* Per seleziona le colonne da visualizzare utilizza l’opzione **Impostazioni vista** sotto il pulsante Viste. È possibile visualizzare le colonne seguenti:

   * **Nome**: nome della pagina, utile in un ambiente di authoring multilingue poiché fa parte dell’URL della pagina e non viene modificato indipendentemente dalla lingua
   * **Modificato**: data dell’ultima modifica e dell’utente che l’ha eseguita
   * **Pubblicato**: stato della pubblicazione
   * **Modello**: modello su cui si basa la pagina
   * **Flusso di lavoro**: flusso di lavoro attualmente applicato alla pagina. Ulteriori informazioni sono disponibili quando passi sopra con il mouse o apri la Timeline.

   * **Dati analitici della pagina**
   * **Visitatori univoci**
   * **Tempo sulla pagina**

  ![Impostazioni vista - Configura colonne](assets/bh-21.png)

  Per impostazione predefinita, la colonna **Nome** è visualizzata e costituisce una porzione dell’URL della pagina. In alcuni casi, l’autore potrebbe dover accedere a pagine in una lingua diversa e la visualizzazione del nome della pagina (che di solito è immutabile) può essere di grande aiuto se l’autore non conosce la lingua della pagina.

* Cambia l’ordine degli elementi utilizzando la barra verticale punteggiata all’estrema destra di ciascun elemento dell’elenco.

  >[!NOTE]
  >
  >La modifica dell’ordine funziona solo all’interno di una cartella ordinata il cui valore `jcr:primaryType` è impostato su `sling:OrderedFolder`.

  ![Cambia ordine](assets/bh-22.png)

  Tocca o fai clic sulla barra di selezione verticale e trascina l’elemento in una nuova posizione nell’elenco.

  ![Ordine di modifica - Trascina](assets/bh-23.png)

* Puoi visualizzare i dati di Analytics visualizzando le colonne appropriate utilizzando **Impostazioni vista** .

  Puoi filtrare i dati di Analytics per gli ultimi 30, 90 o 365 giorni utilizzando le opzioni di filtro sul lato destro dell’intestazione.

  ![Analytics](assets/bh-24.png)

## Selettore della barra {#rail-selector}

Il **selettore della barra** è disponibile in alto a sinistra nella finestra e visualizza opzioni che dipendono dalle console correnti.

![Selettore della barra](assets/bh-25.png)

Ad esempio, in Sites puoi selezionare solo il contenuto (opzione predefinita), la struttura del contenuto, la timeline, i riferimenti o il pannello laterale del filtro.

Se selezioni solo il contenuto, appare solo l’icona della barra. Quando selezioni qualsiasi altra opzione, il nome è visualizzato accanto all’icona della barra.

>[!NOTE]
>
>Sono disponibili [scelte rapide da tastiera](/help/sites-authoring/keyboard-shortcuts.md) per passare rapidamente da un’opzione all’altra della barra.

### Struttura contenuto {#content-tree}

La struttura del contenuto può essere utilizzata per spostarsi rapidamente nella gerarchia del sito all’interno del pannello laterale e visualizzare molte informazioni sulle pagine nella cartella corrente.

Utilizzando il pannello laterale della struttura del contenuto insieme a una vista a elenco o a schede, gli utenti possono facilmente vedere la struttura gerarchica del progetto e spostarsi facilmente all’interno della struttura del contenuto con il pannello laterale della struttura del contenuto, nonché visualizzare informazioni di pagina dettagliate nella vista a elenco.

![Struttura contenuto](assets/bh-26.png)

>[!NOTE]
>
>Una volta selezionata una voce nella visualizzazione gerarchica, puoi spostarti rapidamente nella gerarchia attraverso i tasti freccia.
>
>Consulta la sezione [scelte rapide da tastiera](/help/sites-authoring/keyboard-shortcuts.md) per ulteriori informazioni.

### Timeline  {#timeline}

La timeline può essere utilizzata per visualizzare e/o avviare eventi che si sono verificati sulla risorsa selezionata. Per aprire la colonna della timeline, utilizza il selettore della barra a sinistra:

La colonna della timeline consente di:

* [Visualizzare vari eventi relativi all’elemento selezionato.](#timelineviewevents)

   * I tipi di evento possono essere selezionati dall’elenco a discesa:

      * [Commenti](#timelineaddingandviewingcomments)
      * Annotazioni
      * Attività
      * [Lanci](/help/sites-authoring/launches.md)
      * [Versioni](/help/sites-authoring/working-with-page-versions.md)
      * [Flussi di lavoro](/help/sites-authoring/workflows-applying.md)

         * ad eccezione di [flussi di lavoro transitori](/help/sites-developing/workflows.md#transient-workflows) poiché non vengono salvate informazioni sulla cronologia per questi

      * e Mostra tutto

* [Aggiungere o visualizzare commenti sulla voce selezionata. ](#timelineaddingandviewingcomments) La casella **Commento** è visualizzata in fondo all’elenco degli eventi. Per registrare un commento, digitalo e premi Invio. Il commento verrà visualizzato quando selezioni **Commenti** o **Mostra tutto**.

* Alcune console offrono funzionalità aggiuntive. Ad esempio, nella console Sites è possibile:

   * [Salvare una versione](/help/sites-authoring/working-with-page-versions.md#creatinganewversiontouchoptimizedui).
   * [Avviare un flusso di lavoro](/help/sites-authoring/workflows-applying.md#startingaworkflowfromtherail).

Queste opzioni sono accessibili tramite la freccia accanto al **Commento** campo.

![Timeline](assets/bh-27.png)

### Riferimenti {#references}

**I riferimenti mostrano eventuali collegamenti alla risorsa selezionata.** Ad esempio, nella console **Sites**, i [riferimenti](/help/sites-authoring/author-environment-tools.md#showingpagereferences) per le pagine mostrano:

* [Lanci](/help/sites-authoring/launches.md#launches-in-references-sites-console)
* [Live Copy](/help/sites-administering/msm-livecopy-overview.md#openingthelivecopyoverviewfromreferences)
* [Copie per lingua](/help/sites-administering/tc-prep.md#seeing-the-status-of-language-roots)
* Riferimenti ai contenuti:

   * collegamenti da altre pagine alla pagina selezionata
   * contenuto preso in prestito da e/o prestato alla pagina selezionata dal componente Riferimento

![bh-28](assets/bh-28.png)

### Filtro {#filter}

Verrà aperto un pannello simile alla [Ricerca](/help/sites-authoring/search.md) con i filtri di posizione già impostati, che consentono di filtrare ulteriormente il contenuto da visualizzare.

![Filtro](assets/bh-29.png)
