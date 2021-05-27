---
title: Operazioni di base
seo-title: Operazioni di base
description: Acquisisci dimestichezza con AEM e le funzioni di base
seo-description: Acquisisci dimestichezza con AEM e le funzioni di base
uuid: c78ef9da-e0bd-47be-a410-9cf2ae71749a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 21181a6f-b434-40ed-8eb1-ebdfc98964dd
docset: aem65
exl-id: ef1a3997-feb4-4cb0-9396-c8335b69bb10
source-git-commit: 440aa5a2f4a020a16104f11eaf484a2cf7291e1f
workflow-type: tm+mt
source-wordcount: '2980'
ht-degree: 95%

---

# Operazioni di base{#basic-handling}

>[!NOTE]
>
>* Questa pagina offre una panoramica delle operazioni di base nell’ambiente di creazione AEM. Usa la console **Sites** come base.
   >
   >
* Alcune funzionalità non sono disponibili su tutte le console e in alcune console potrebbero essere disponibili funzionalità aggiuntive. In altre sezioni puoi trovare informazioni specifiche sulle singole console e le relative funzionalità.
>* AEM supporta l’utilizzo di scelte rapide da tastiera in numerose aree, in particolare per l’[utilizzo delle console](/help/sites-authoring/keyboard-shortcuts.md) e la [modifica delle pagine](/help/sites-authoring/page-authoring-keyboard-shortcuts.md).

>



## Guida introduttiva {#getting-started}

### Interfaccia touch {#a-touch-enabled-ui}

L’interfaccia utente di AEM è dotata di funzionalità touch. Un’interfaccia touch consente di interagire con il software con azioni come toccare, tenere premuto e scorrere. Questa modalità di funzionamento è diversa da quella di un’interfaccia desktop tradizionale, che prevede azioni del mouse come clic, doppio clic, clic con il pulsante destro del mouse e passaggio del cursore del mouse.

Siccome l’interfaccia utente AEM è abilitata alle funzioni touch, puoi utilizzare i movimenti touch sui dispositivi che li supportano (ad esempio, smartphone o tablet) e le azioni del mouse su un dispositivo desktop tradizionale.

### Primi passi {#first-steps}

Immediatamente dopo aver effettuato l’accesso, si aprirà il pannello di [navigazione](#navigation-panel). Selezionando una delle opzioni si apre la rispettiva console.

![bh-01](assets/bh-01.png)

>[!NOTE]
>
>Per illustrare l’utilizzo di base di AEM, in questo documento viene utilizzata la console **Sites.**
>
>Tocca o fai clic su **Sites** per iniziare.

### Navigazione nel prodotto  {#product-navigation}

Ogni volta che un utente accede per la prima volta a una console, viene avviata un’esercitazione relativa alla navigazione nel prodotto. Dedica alcuni minuti all’esercitazione per ottenere una buona panoramica dell’utilizzo di base di AEM.

![bh-02](assets/bh-02.png)

Tocca o fai clic su **Avanti** per passare alla pagina successiva della panoramica. Tocca o fai clic su **Chiudi** oppure tocca o fai clic all’esterno della finestra di dialogo della panoramica per chiuderla.

Se non visualizzi tutte le slide o non selezioni l’opzione **Non mostrare più**, la panoramica viene riavviata la prossima volta che accedi a una console.

## Navigazione globale {#global-navigation}

È possibile spostarsi tra le console utilizzando il pannello di navigazione globale. Questo è attivato come elenco a discesa a schermo intero quando tocchi o fai clic sul collegamento Adobe Experience Manager in alto a sinistra.

Per chiudere il pannello di navigazione globale e tornare alla posizione precedente, tocca o fai clic su **Chiudi**.

![bh-03](assets/bh-03.png)

>[!NOTE]
>
>Al primo accesso ti è stato mostrato il pannello di **navigazione**.

La navigazione globale presenta due pannelli, rappresentati da icone sul lato sinistro dello schermo:

* **[Navigazione](/help/sites-authoring/basic-handling.md#navigation-panel)**: rappresentata da una bussola 
* **[Strumenti](/help/sites-authoring/basic-handling.md#tools-panel)**: rappresentati da un martello

Le opzioni disponibili in questi pannelli sono descritte di seguito.

### Pannello di navigazione   {#navigation-panel}

Il pannello Navigazione consente di accedere alle console AEM:

![bh-01](assets/bh-01.png)

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
   <td>Queste console consentono di importare e <a href="/help/assets/home.md">gestire le risorse digitali</a> quali immagini, video, documenti e file audio. Puoi usare queste risorse da qualunque sito web in esecuzione nell’istanza di AEM. </td>
  </tr>
  <tr>
   <td>Communities</td>
   <td>Questa console permette di creare e gestire <a href="/help/communities/sites-console.md">siti di community</a> a scopo di <a href="/help/communities/overview.md#engagement-community">coinvolgimento</a> e <a href="/help/communities/overview.md#enablement-community">abilitazione</a> degli utenti.</td>
  </tr>
  <tr>
   <td>Commerce</td>
   <td>Questa console consente di gestire prodotti, cataloghi di prodotti e ordini relativi ai siti <a href="/help/commerce/cif-classic/administering/ecommerce.md">Commerce</a>.</td>
  </tr>
  <tr>
   <td>Frammenti di esperienza</td>
   <td>Un frammento di esperienza<a href="/help/sites-authoring/experience-fragments.md"> è un’esperienza autonoma che può essere riutilizzata su tutti i canali, supporta le varianti e non richiede di copiare e incollare le esperienze o parti di esse.</a></td>
  </tr>
  <tr>
   <td>Forms</td>
   <td>Questa console permette di creare, gestire ed elaborare <a href="/help/forms/home.md">moduli e documenti</a>.</td>
  </tr>
  <tr>
   <td>Personalizzazione</td>
   <td>Questa console fornisce un <a href="/help/sites-authoring/personalization.md">set di strumenti per la creazione e modifica di contenuti mirati e la presentazione di esperienze personali</a>.</td>
  </tr>
  <tr>
   <td>Progetti</td>
   <td>La <a href="/help/sites-authoring/touch-ui-managing-projects.md">console Progetti offre accesso diretto ai tuoi progetti</a>, che sono dashboard virtuali. Possono essere usati per creare un team di persone con obiettivi comuni e consentire al team di accedere a risorse, flussi di lavoro e attività. <br /> </td>
  </tr>
  <tr>
   <td>Screens</td>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/authoring/setting-up-projects/creating-a-screens-project.html">Screens</a> consente di gestire tutti gli schermi, di qualsiasi dimensione, che verranno utilizzati dai clienti.</td>
  </tr>
  <tr>
   <td>Sites</td>
   <td>Le console Sites ti permettono di <a href="/help/sites-authoring/page-authoring.md">creare, visualizzare e gestire siti web</a> in esecuzione sull’istanza AEM. Da queste console puoi creare, modificare, copiare, spostare ed eliminare pagine di siti web, avviare flussi di lavoro e pubblicare pagine.<br /> </td>
  </tr>
 </tbody>
</table>

### Pannello Strumenti {#tools-panel}

Nel pannello Strumenti, tutte le opzioni nel pannello laterale contengono una serie di sottomenu. Le [console Strumenti](/help/sites-administering/tools-consoles.md) disponibili in questo pannello permettono di accedere a console e strumenti specifici per la gestione dei siti web, delle risorse digitali e altri aspetti dell’archivio dei contenuti.

![bh-04](assets/bh-04.png)

## Intestazione {#the-header}

L’intestazione è sempre presente nella parte superiore dello schermo. Anche se la maggior parte delle opzioni presenti nell’intestazione rimangono invariate ovunque ti trovi nel sistema, alcune dipendono dal contesto.

![bh-05](assets/bh-03.png)

* [Navigazione globale](#navigatingconsolesandtools)

   Seleziona il collegamento **Adobe Experience Manager** per spostarti tra le diverse console.

   ![screen_shot_2018-03-23at103615](assets/screen_shot_2018-03-23at103615.png)

* [Ricerca](/help/sites-authoring/search.md)

   ![](do-not-localize/screen_shot_2018-03-23at103542.png)

   È anche possibile utilizzare il [tasto di scelta rapida](/help/sites-authoring/keyboard-shortcuts.md) `/` (barra obliqua) per richiamare la ricerca da qualsiasi console.

* [Soluzioni](https://www.adobe.com/it/experience-cloud.html)

   ![](do-not-localize/screen_shot_2018-03-23at103552.png)

* [Aiuto](#accessinghelptouchoptimizedui)

   ![](do-not-localize/screen_shot_2018-03-23at103547.png)

* [Notifiche](/help/sites-authoring/inbox.md)

   ![](do-not-localize/screen_shot_2018-03-23at103558.png)

   Questa icona viene contrassegnata con il numero di notifiche incomplete attualmente assegnate.

   >[!NOTE]
   >
   >AEM viene fornito con attività amministrative preconfigurate assegnate al gruppo degli utenti amministratore. Per ulteriori informazioni, vedi [Attività amministrative pronte all’uso](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks).

* [Proprietà utente](/help/sites-authoring/user-properties.md)

   ![](do-not-localize/screen_shot_2018-03-23at103603.png)

* [Selettore della barra](/help/sites-authoring/basic-handling.md#rail-selector)

   ![](do-not-localize/screen_shot_2018-03-23at103943.png)

   Le opzioni visualizzate dipendono dalla console corrente. Ad esempio, in **Siti** potete selezionare solo il contenuto (opzione predefinita), la timeline, i riferimenti o il pannello laterale del filtro.

   ![screen_shot_2018-03-23at104029](assets/screen_shot_2018-03-23at104029.png)

* Breadcrumb

   ![bh-05](assets/bh-05.png)

   Situate al centro della barra, le breadcrumb mostrano sempre la descrizione dell’elemento attualmente selezionato e consentono di spostarsi all’interno di una console specifica. Nella console Sites puoi spostarti tra i vari livelli del sito web.

   Ti basterà fare clic sul testo della breadcrumb per visualizzare un elenco a discesa con i livelli della gerarchia dell’elemento selezionato. Fai clic su una voce per passare a tale posizione.

   ![bh-06](assets/bh-06.png)

* Selezione del periodo di tempo per l’analisi

   ![screen_shot_2018-03-23at104126](assets/screen_shot_2018-03-23at104126.png)

   Questa funzione è disponibile solo nella vista a elenco. Per ulteriori informazioni, consulta [Vista a elenco](#list-view) .

* Pulsante **Crea**

   ![screen_shot_2018-03-23at104301](assets/screen_shot_2018-03-23at104301.png)

   Dopo che hai fatto clic, le opzioni visualizzate sono adatte alla console/al contesto.

* [Viste](/help/sites-authoring/basic-handling.md#viewingandselectingyourresourcescardlistcolumn)

   L’icona di visualizzazione si trova all’estrema destra della barra degli strumenti di AEM. Inoltre, indica la vista corrente e ne consente la modifica. Ad esempio, la visualizzazione predefinita **Vista a colonne** presenta questa icona:

   ![bh-07](assets/bh-07.png)

   Puoi alternare tra le viste a colonne, a schede e a elenco; la vista a elenco mostra anche le impostazioni di visualizzazione.

   ![bh-09](assets/bh-09.png)

* Navigazione tramite tastiera

   Potete navigare in un sito web utilizzando solo la tastiera. Questo utilizza la funzionalità standard del browser del tasto **TAB** (o **OPT+TAB**) per spostarti tra gli elementi della pagina che sono *focalizzabili*.

   Nella console di **Sites** è stata aggiunta l’opzione per **passare al contenuto principale**. Questo diventa visibile mentre si passa alla *scheda* tra le opzioni di intestazione e accelera la navigazione consentendo di saltare gli elementi standard nella barra degli strumenti (prodotto) e di passare direttamente al contenuto principale.

   ![bh-30](assets/bh-30.png)

## Accedere all’Aiuto {#accessing-help}

Sono disponibili diverse risorse di Aiuto:

* **Barra degli strumenti della console**

   A seconda di dove ti trovi nell’applicazione, l’icona **Aiuto** consente di accedere alle risorse appropriate:

   ![bh-10](assets/bh-10.png)

* **Navigazione**

   La prima volta che accedi al sistema, compare [una serie di diapositive introduttive su come navigare in AEM](/help/sites-authoring/basic-handling.md#product-navigation).

* **Editor pagina**

   La prima volta che modifichi una pagina, compare una serie di diapositive introduttive sull’editor pagina.

   ![bh-11](assets/bh-11.png)

   Esamina questa panoramica come faresti con la [panoramica di navigazione del prodotto](/help/sites-authoring/basic-handling.md#product-navigation) la prima volta che accedi a una console.

   Dal menu [**Informazioni sulle pagine** puoi selezionare **Aiuto**](/help/sites-authoring/author-environment-tools.md#accessing-help) per accedervi di nuovo in un secondo tempo.

* **Console Strumenti**

   Dalla console **Strumenti** puoi inoltre accedere ai **Riferimenti** esterni:

   * **Documentazione** Visualizza la documentazione per la gestione delle esperienze web

   * **Risorse per sviluppatori** Risorse per sviluppatori e download
   >[!NOTE]
   >
   >Puoi accedere in qualsiasi momento ai tasti di scelta rapida, semplicemente utilizzando il tasto di scelta rapida `?` (punto interrogativo) all’interno della console.
   >
   >Per una panoramica di tutte le scelte rapide da tastiera, consulta la documentazione seguente:
   >
   >    * [Scelte rapide da tastiera per la modifica delle pagine](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [Scelte rapide da tastiera per le console](/help/sites-authoring/keyboard-shortcuts.md)


## Barra delle azioni   {#actions-toolbar}

Ogni volta che selezioni una risorsa (ad esempio una pagina o una risorsa), le icone indicano diverse azioni, con testo descrittivo nella barra degli strumenti. Queste azioni dipendono da:

* La console corrente.
* Il contesto attuale.
* Se sei o meno in modalità [Selezione](#navigatingandselectionmode).

L’azione disponibile nella barra degli strumenti varia per riflettere le azioni che puoi eseguire sugli oggetti specifici selezionati.

La modalità di [selezione di una risorsa](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) dipende dalla vista.

A causa del poco spazio disponibile in alcune finestre, la barra può facilmente superare lo spazio a disposizione. In questo caso compaiono altre opzioni. Tocca o fai clic sui tre puntini (**...**) per aprire un selettore a discesa contenente tutte le azioni che non rientrano nella barra. Ad esempio, dopo la selezione di una pagina nella console **Sites**:

![Barra delle azioni ](assets/bh-12.png)

>[!NOTE]
Le singole icone disponibili sono documentate in relazione alla console, alla funzione o allo scenario appropriato.

## Azioni rapide   {#quick-actions}

Nella [Vista a schede](#cardviewquickactions) alcune azioni sono disponibili come icone di scelta rapida, oltre che dalla barra degli strumenti. Le icone delle azioni rapide sono disponibili per un elemento alla volta ed evitano di dover preselezionare le opzioni.

La azioni rapide sono visibili con un tocco prolungato (su dispositivo touch) sulla scheda di una risorsa. Le azioni rapide disponibili dipendono dalla console e dal contesto. Ad esempio, di seguito sono riportate le azioni rapide per una pagina nella console **Sites**:

![bh-13](assets/bh-13.png)

## Visualizzazione e selezione delle risorse {#viewing-and-selecting-resources}

In tutte le viste la visualizzazione, la navigazione e la selezione funzionano allo stesso modo, ma con lievi variazioni a seconda della vista attiva.

Puoi visualizzare, navigare e selezionare (per ulteriori azioni) le risorse in una qualsiasi delle viste disponibili, selezionabili dall’icona in alto a destra:

* [Vista a colonne](#column-view)
* [Vista a schede](#card-view)

* [Vista a elenco ](#list-view)

>[!NOTE]
Per impostazione predefinita, AEM Assets non visualizza le rappresentazioni originali delle risorse nell’interfaccia utente come miniature in nessuna delle viste. Se sei un amministratore, puoi utilizzare le sovrapposizioni per configurare AEM Assets in modo da visualizzare le rappresentazioni originali come miniature.

### Selezionare le risorse   {#selecting-resources}

La selezione di una specifica risorsa dipende dalla combinazione della vista e del dispositivo utilizzati:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td>Selezionare</td>
   <td>Deselezionare</td>
  </tr>
  <tr>
   <td>Vista a colonne<br /> </td>
   <td>
    <ul>
     <li>Desktop: <br /> Fate clic sulla miniatura</li>
     <li>Dispositivo mobile: <br /> Fate clic sulla miniatura</li>
    </ul> </td>
   <td>
    <ul>
     <li>Desktop: <br /> Fate clic sulla miniatura</li>
     <li>Dispositivo mobile: <br /> Fate clic sulla miniatura</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Vista a schede<br /> </td>
   <td>
    <ul>
     <li>Desktop:<br /> Passate il puntatore del mouse, quindi utilizzate l'azione rapida con il segno di spunta</li>
     <li>Dispositivo mobile: <br /> Tenete premuto sulla scheda</li>
    </ul> </td>
   <td>
    <ul>
     <li>Desktop:<br /> Fai clic sulla scheda</li>
     <li>Dispositivo mobile:<br /> Toccate la scheda</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Vista a elenco </td>
   <td>
    <ul>
     <li>Desktop: <br /> Fate clic sulla miniatura</li>
     <li>Dispositivo mobile: <br /> Fate clic sulla miniatura</li>
    </ul> </td>
   <td>
    <ul>
     <li>Desktop: <br /> Fate clic sulla miniatura</li>
     <li>Dispositivo mobile: <br /> Fate clic sulla miniatura</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Seleziona tutto {#select-all}

Per selezionare tutti gli elementi in qualsiasi vista, fai clic sull’opzione **Seleziona tutto** nell’angolo in alto a destra della console.

* Nella **Vista a schede**, vengono selezionate tutte le schede.
* Nella **Vista a elenco**, vengono selezionati tutti gli elementi dell’elenco.
* Nella **Vista a colonne**, vengono selezionati tutti gli elementi nella colonna più a sinistra.

![screen-shot_2019-03-05at094659](assets/screen-shot_2019-03-05at094659.png)

#### Deselezionare tutti gli elementi {#deselecting-all}

In tutti i casi in cui selezioni elementi, il numero degli elementi selezionati viene visualizzato in alto a destra nella barra degli strumenti.

Per deselezionare tutti gli elementi e uscire dalla modalità di selezione, puoi fare una delle seguenti operazioni:

* Tocca o fai clic sulla **X** accanto al conteggio. 

* Premi **Esc**.

![bh-14](assets/bh-14.png)

In tutte le viste, tutti gli elementi possono essere deselezionati con il tasto Esc, se utilizzi un dispositivo desktop.

#### Esempio di selezione {#selecting-example}

1. Ad esempio, nella vista a schede:

   ![bh-15](assets/bh-15.png)

1. Dopo la selezione di una risorsa, l’intestazione superiore è coperta dalla [barra delle azioni](#actionstoolbar), che permette di accedere alle azioni applicabili alla risorsa selezionata.

   Per uscire dalla modalità di selezione, seleziona la **X** in alto a destra oppure premi **Esc**.

### Vista a colonne {#column-view}

![bh-16](assets/bh-16.png)

La vista a colonne consente la navigazione visiva in una struttura di contenuti tramite una serie di colonne in cascata. Consente di visualizzare e scorrere la struttura ad albero del sito web.

Quando si seleziona una risorsa nella prima colonna a sinistra, vengono visualizzate le risorse secondarie in una colonna a destra. Quando si seleziona una risorsa nella colonna a destra, vengono visualizzate le risorse secondarie in un’altra colonna a destra, e così via.

* Per spostarti in alto e in basso nella struttura ad albero, tocca o fai clic sul nome di una risorsa o sulla freccia a destra del nome.

   * Il nome della risorsa e la freccia vengono evidenziati quando tocchi o fai clic su tali elementi.

   ![bh-17](assets/bh-17.png)

   * Gli elementi figlio della risorsa che hai toccato o su cui hai fatto clic vengono visualizzati nella colonna a destra di tale risorsa.
   * Se tocchi o fai clic sul nome di una risorsa che non presenta elementi figlio, i relativi dettagli verranno visualizzati nella colonna finale.


* Quando tocchi o fai clic sulla miniatura, la risorsa viene selezionata.

   * Quando una risorsa è selezionata, compare un segno di spunta sulla miniatura e il nome della risorsa viene evidenziato.
   * I dettagli della risorsa selezionata sono visualizzati nella colonna finale.
   * La barra delle azioni diventerà disponibile.

   ![bh-18](assets/bh-18.png)

   Quando una pagina viene selezionata nella vista a colonne, viene visualizzata nella colonna finale con i seguenti dettagli:

   * Titolo pagina
   * Nome pagina (parte dell’URL della pagina)
   * Modello su cui si basa la pagina
   * Dettagli di modifica
   * Lingua della pagina
   * Dettagli di pubblicazione


### Vista a schede {#card-view}

![bh-15-1](assets/bh-15-1.png)

* La vista a schede mostra schede informative per ogni elemento al livello corrente, che forniscono informazioni quali:

   * Una rappresentazione visiva del contenuto della pagina.
   * Il titolo della pagina.
   * Date importanti (ad esempio ultima modifica, ultima pubblicazione).
   * Se la pagina è bloccata, nascosta o fa parte di una Live Copy.
   * Se appropriato, quando devi eseguire un’azione nell’ambito di un flusso di lavoro.

      * Alle voci della [Casella in entrata](/help/sites-authoring/inbox.md) possono essere correlati dei marcatori che indicano le azioni necessarie.

* In questa vista sono disponibili anche [azioni rapide](#quick-actions), per effettuare selezioni ed, eseguire le operazioni più comuni, come la modifica.

   ![bh-13-1](assets/bh-13-1.png)

* Per spostarti verso il basso nella struttura, tocca o fai clic sulle schede (facendo attenzione a evitare le azioni rapide); per tornare verso l’alto utilizza le [breadcrumb nell’intestazione](/help/sites-authoring/basic-handling.md#the-header).

### Vista a elenco   {#list-view}

![bh-19](assets/bh-19.png)

* Nella vista a elenco sono elencate le informazioni di ogni risorsa al livello corrente.
* Per spostarti verso il basso nella struttura, tocca o fai clic sul nome delle risorse; per tornare verso l’alto utilizza le [breadcrumb nell’intestazione](/help/sites-authoring/basic-handling.md#the-header).

* Per selezionare tutti gli elementi nell’elenco, utilizza la casella di selezione in alto a sinistra nell’elenco.

   ![bh-20](assets/bh-20.png)

   * Quando tutti gli elementi dell’elenco sono selezionati, questa casella è selezionata.

      * Tocca o fai clic sulla casella di selezione per deselezionare tutti gli elementi.
   * Se sono selezionati solo alcuni elementi, viene visualizzato un segno meno (-).

      * Tocca o fai clic sulla casella di selezione per selezionare tutti gli elementi.
      * Tocca o fai clic nuovamente sulla casella di selezione per deselezionare tutti gli elementi.


* Per seleziona le colonne da visualizzare utilizza l’opzione **Impostazioni vista** sotto il pulsante Viste. È possibile visualizzare le colonne seguenti:

   * **Nome**: nome della pagina, utile in un ambiente di authoring multilingue poiché fa parte dell’URL della pagina e non viene modificato indipendentemente dalla lingua
   * **Modificato**: data dell’ultima modifica e dell’utente che l’ha eseguita
   * **Pubblicato**: stato della pubblicazione
   * **Modello**: modello su cui si basa la pagina
   * **Flusso di lavoro**: flusso di lavoro attualmente applicato alla pagina. Ulteriori informazioni sono disponibili quando passi sopra con il mouse o apri la Timeline.

   * **Dati analitici pagina**
   * **Visitatori univoci**
   * **Tempo sulla pagina**

   ![bh-21](assets/bh-21.png)

   Per impostazione predefinita, la colonna **Nome** è visualizzata e costituisce una porzione dell’URL della pagina. In alcuni casi, l’autore potrebbe dover accedere a pagine in una lingua diversa; poiché il nome della pagina di solito non cambia, può essere di grande aiuto se si tratta di una lingua che l’autore non conosce.

* Cambia l’ordine degli elementi utilizzando la barra verticale punteggiata all’estrema destra di ciascun elemento dell’elenco.

   >[!NOTE]
   La modifica dell’ordine funziona solo all’interno di una cartella ordinata il cui valore `jcr:primaryType` è impostato su `sling:OrderedFolder`.

   ![bh-22](assets/bh-22.png)

   Tocca o fai clic sulla barra di selezione verticale e trascina l’elemento in una nuova posizione nell’elenco.

   ![bh-23](assets/bh-23.png)

* Puoi visualizzare i dati Analisi visualizzando le colonne appropriate tramite la finestra di dialogo delle **Impostazioni di visualizzazione**.

   Puoi filtrare i dati Analisi degli ultimi 30, 90 o 365 giorni mediante le opzioni filtro a destra dell’intestazione.

   ![bh-24](assets/bh-24.png)

## Selettore della barra {#rail-selector}

Il **selettore della barra** è disponibile in alto a sinistra nella finestra e visualizza opzioni che dipendono dalle console correnti.

![bh-25](assets/bh-25.png)

Ad esempio, in Sites puoi selezionare solo il contenuto (opzione predefinita), la struttura del contenuto, la timeline, i riferimenti o il pannello laterale del filtro.

Se selezioni solo il contenuto, appare solo l’icona della barra. Quando selezioni qualsiasi altra opzione, il nome è visualizzato accanto all’icona della barra.

>[!NOTE]
Sono disponibili [scelte rapide da tastiera](/help/sites-authoring/keyboard-shortcuts.md) per passare rapidamente da un’opzione all’altra della barra.

### Struttura contenuto {#content-tree}

La struttura del contenuto può essere utilizzata per spostarsi rapidamente nella gerarchia del sito all’interno del pannello laterale e visualizzare molte informazioni sulle pagine nella cartella attuale.

Mediante il pannello laterale della struttura del contenuto, insieme alla vista a elenco o a schede, gli utenti possono visualizzare facilmente la struttura gerarchica del progetto ed esplorare in modo più semplice la struttura del contenuto, nonché visualizzare informazioni dettagliate sulla pagina nella vista a elenco.

![bh-26](assets/bh-26.png)

>[!NOTE]
Una volta selezionata una voce nella visualizzazione gerarchica, puoi spostarti rapidamente nella gerarchia attraverso i tasti freccia.
Per ulteriori informazioni, vedi le [scelte rapide da tastiera](/help/sites-authoring/keyboard-shortcuts.md).

### Timeline  {#timeline}

Con la timeline puoi visualizzare e/o attivare gli eventi della risorsa selezionata. Per aprire la colonna della timeline, utilizza il selettore della barra a sinistra:

La colonna della timeline consente di effettuare le seguenti operazioni:

* [Visualizzare vari eventi relativi all’elemento selezionato.](#timelineviewevents)

   * I tipi di evento possono essere selezionati dall’elenco a discesa:

      * [Commenti](#timelineaddingandviewingcomments)
      * Annotazioni
      * Attività
      * [Lanci](/help/sites-authoring/launches.md)
      * [Versioni](/help/sites-authoring/working-with-page-versions.md)
      * [Flussi di lavoro](/help/sites-authoring/workflows-applying.md)

         * ad eccezione dei [flussi di lavoro transitori](/help/sites-developing/workflows.md#transient-workflows), in quanto per tali flussi non vengono conservate informazioni sulla cronologia
      * e Mostra tutto


* [Aggiungere o visualizzare commenti sulla voce selezionata. ](#timelineaddingandviewingcomments) La casella **Commento** è visualizzata in fondo all’elenco degli eventi. Per registrare un commento, digitalo e premi Invio. Il commento verrà visualizzato quando selezioni **Commenti** o **Mostra tutto**.

* Alcune console offrono funzionalità aggiuntive. Ad esempio, nella console Sites è possibile:

   * [Salvare una versione](/help/sites-authoring/working-with-page-versions.md#creatinganewversiontouchoptimizedui).
   * [Avviare un flusso di lavoro](/help/sites-authoring/workflows-applying.md#startingaworkflowfromtherail).

Queste opzioni sono accessibili tramite la freccia accanto al campo **Commento**.

![bh-27](assets/bh-27.png)

### Riferimenti {#references}

**I riferimenti mostrano eventuali collegamenti alla risorsa selezionata.** Ad esempio, nella console **Sites** i [riferimenti](/help/sites-authoring/author-environment-tools.md#showingpagereferences) per le pagine visualizzano:

* [Lanci](/help/sites-authoring/launches.md#launches-in-references-sites-console)
* [Live Copy](/help/sites-administering/msm-livecopy-overview.md#openingthelivecopyoverviewfromreferences)
* [Copie per lingua](/help/sites-administering/tc-prep.md#seeing-the-status-of-language-roots)
* Riferimenti ai contenuti:

   * Collegamenti da altre pagine alla pagina selezionata
   * Contenuti presi in prestito da e/o prestati alla pagina selezionata dal componente Riferimento

![bh-28](assets/bh-28.png)

### Filtro {#filter}

Verrà aperto un pannello simile alla [Ricerca](/help/sites-authoring/search.md) con i filtri di posizione già impostati, che consentono di filtrare ulteriormente il contenuto da visualizzare.

![bh-29](assets/bh-29.png)
