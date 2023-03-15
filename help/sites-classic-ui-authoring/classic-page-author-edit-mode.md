---
title: Componenti per l’authoring delle pagine
seo-title: Components for Page Authoring
description: I componenti sono disponibili quando si modifica una pagina dalla scheda Componenti della barra laterale, utilizzando il selettore Inserisci nuovo componente (con doppio clic nell’area Trascina qui i componenti o le risorse).
seo-description: The components are available when editing a page from the Components tab of the sidekick and the Insert New Component selector (when you double-click in the Drag components or assets here area).
uuid: c353073d-d4d1-4529-b8bd-d0ca302cc9a0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9aa0521f-f321-42e9-b022-7ff968a36212
docset: aem65
exl-id: 88af99df-846b-47b3-9b1f-68bfdfc40eb8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6133'
ht-degree: 86%

---

# Componenti per l’authoring delle pagine{#components-for-page-authoring}

I componenti seguenti sono destinati a essere utilizzati durante l’authoring di contenuti per una pagina web standard. Costituiscono un sottoinsieme dei componenti disponibili per un’installazione standard di AEM.

Alcuni sono immediatamente disponibili nella barra laterale, altri anche utilizzando la [modalità di progettazione](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md) per attivarli/disattivarli.

>[!CAUTION]
>
>Questa sezione illustra unicamente i componenti disponibili pronti all’uso in un’installazione AEM standard.
>
>A seconda dell’istanza corrente è possibile che siano presenti componenti personalizzati sviluppati esplicitamente per le tue esigenze. Questi possono anche avere lo stesso nome di alcuni dei componenti qui descritti.

I componenti sono disponibili quando [modifica di una pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) dal **Componenti** scheda della barra laterale e **Inserisci nuovo componente** selettore (quando fai doppio clic nel **Trascina qui i componenti o le risorse** area).

Puoi selezionare un componente e trascinarlo nella posizione desiderata sulla pagina, quindi [Modifica contenuto e proprietà](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties).

I componenti sono ordinati in base a varie categorie (gruppi di componenti), che comprendono (per l’authoring delle pagine):

* [Generale](#general): include i componenti di base tra cui testo, immagini, tabelle, grafici e così via.
* [Colonne](#columns): include i componenti che consentono di organizzare il layout dei contenuti.
* [Modulo](#formgroup): include tutti i componenti necessari alla creazione di moduli.

## Generale {#general}

I componenti del gruppo Generale sono i componenti di base utilizzati per creare contenuti.

### Elemento account {#account-item}

È possibile definire un collegamento con titolo e descrizione.

![](do-not-localize/chlimage_1-2.png)

### Immagine adattiva {#adaptive-image}

Il componente Immagine adattiva genera immagini che vengono ridimensionate in base alla finestra nella quale viene aperta la pagina web. Per utilizzare questo componente, occorre fornire una risorsa immagine dal file system o DAM. Quando la pagina web viene aperta, il browser scarica una copia dell’immagine ridimensionata, adatta per la finestra corrente.

Le dimensioni della finestra dipendono dalle seguenti caratteristiche:

* Schermo del dispositivo: nei dispositivi mobili le pagine web vengono in genere visualizzate a schermo intero.
* Dimensioni della finestra del browser: gli utenti di computer laptop e desktop possono ridimensionare la finestra del browser.

Ad esempio, il componente genera un’immagine piccola quando la pagina web viene aperta da uno smartphone e un’immagine media quando viene aperta da un tablet. Per un portatile, verrà invece creata un’immagine grande se la pagina viene aperta in una finestra del browser con dimensioni massime. Se la finestra del browser viene ridimensionata e ridotta, il componente trasmette un’immagine più piccola e aggiorna la visualizzazione.

#### Formati di immagine supportati {#supported-image-formats}

Per il componente Immagine adattiva puoi usare file immagine con le seguenti estensioni:

* .jpg
* .jpeg
* .png
* .gif &#42;&#42;

>[!CAUTION]
>
>&#42;&#42; I file .gif animati non sono supportati in AEM per le rappresentazioni adattive.

#### Dimensioni e qualità delle immagini {#images-sizes-and-quality}

Nella tabella seguente sono elencati i valori di larghezza immagine generati per determinate larghezze di visualizzazione. L’altezza dell’immagine generata è calcolata in modo da mantenere proporzioni costanti, senza spazi bianchi all’interno del bordo dell’immagine. Per evitare spazi bianchi può essere applicato il ritaglio.

Per le immagini JPEG, la dimensione di visualizzazione può inoltre influenzare la qualità JPEG. Sono possibili le seguenti qualità JPEG:

* Bassa (0,42)
* Media (0,82)
* Alta (1,00)

| Intervallo di larghezza di visualizzazione (pixel) | Larghezza immagine (pixel) | Qualità JPEG | Tipo di dispositivo di destinazione |
|---|---|---|---|
| larghezza &lt;= 319 | 320 | Bassa |  |
| larghezza = 320 | 320 | Media | Smartphone (verticale) |
| 320 &lt; larghezza &lt; 481 | 480 | Media | Smartphone (orizzontale) |
| 480 &lt; larghezza &lt; 769 | 476 | Alta | Tablet (verticale) |
| 768 &lt; larghezza &lt; 1025 | 620 | Alta | Tablet (orizzontale) |
| larghezza &lt;= 1025 | Intera (dimensione originale) | Alta | Desktop |

#### Proprietà {#properties}

La finestra di dialogo consente di modificare le proprietà per l’istanza del componente Immagine adattiva, molte delle quali sono in comune con il componente Immagine, sul quale il primo si basa. Le proprietà sono disponibili in due schede:

* **Immagine**

   * **Immagine** Trascina un’immagine da Content Finder oppure fai clic per aprire una finestra in cui caricare un’immagine. Una volta caricata l’immagine, è possibile ritagliarla, ruotarla o eliminarla. Per ingrandire e ridurre l’immagine, utilizza la barra di scorrimento al di sotto dell’immagine (sopra i pulsanti OK e Annulla)

   * **Ritaglia** Consente di ritagliare un’immagine. Trascina il bordo dell’immagine per ritagliare.

   * **Ruota** Fai clic più volte fino a ottenere la rotazione desiderata.

   * **Cancella** Rimuove l’immagine corrente.

* **Avanzate**

   * **Titolo** Il componente Immagine adattiva non utilizza questa proprietà.

   * **Testo Alt** Testo alternativo per l’immagine.

   * **Collega a** Il componente Immagine adattiva non utilizza questa proprietà.

   * **Descrizione** Il componente Immagine adattiva non utilizza questa proprietà.

#### Estensione del componente Immagine adattiva {#extending-the-adaptive-image-component}

Per informazioni su come personalizzare il componente Immagine adattiva, consulta [Informazioni sul componente Immagine adattiva](/help/sites-developing/responsive.md#using-adaptive-images).

### Carosello {#carousel}

Il componente Carosello consente di visualizzare le immagini associate a singole pagine:

* una per volta
* per un periodo di tempo limitato
* in un ordine specificato
* con un ritardo specificato

I controlli attivi consentono anche di muoversi in sequenza attraverso le pagine visualizzate in tempo reale, a richiesta. Fai clic sull’immagine di pagina visibile per passare alla pagina relativa. In altre parole, il carosello funge da controllo di navigazione.

#### Proprietà {#properties-1}

Sono disponibili in due schede:

* **Carosello** Consente di specificare il funzionamento del carosello:

   * Velocità di riproduzione Tempo in millisecondi prima della visualizzazione della diapositiva successiva.
   * Tempo di transizione Tempo in millisecondi per la transizione tra due dispositive.
   * Stile comandi Varie opzioni sono disponibili tramite un menu a discesa; ad esempio, Pulsanti Prec/Succ, Opzioni alto-destra.

* **Elenco** Consente di specificare in che modo le pagine vengono incluse nel Carosello:

   * **Genera elenco con** Esistono vari modi per generare un elenco di pagine: Pagine figlie, Elenco correzioni, Ricerca o Ricerca avanzata (tutti descritti di seguito). Indipendentemente dal metodo scelto, alle pagine incluse nell’elenco dovrebbe già essere associata un’immagine, che verrà visualizzata nel Carosello. Se a una determinata pagina, nelle Proprietà pagina, non è associata un’immagine, è necessario eseguire l’associazione prima di iniziare, in caso contrario nel Carosello sarà visualizzata una pagina vuota (o quasi completamente vuota). Consulta [Modifica delle Proprietà pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md). A seconda dell’elemento scelto sarà visualizzato un nuovo pannello:

      * **Opzioni per le pagine secondarie**

         * **Pagina padre** Consente di specificare il percorso manualmente o utilizzando il selettore. Non specificare nulla per utilizzare la pagina corrente come pagina padre.
      * **Opzioni per elenco fisso**

         * **Pagine**
Seleziona un elenco di pagine. Utilizzo 
`+` per aggiungere altre voci e i pulsanti su/giù per regolare l&#39;ordine.
      * **Opzioni per la ricerca**

         * **Inizia in** Consente di immettere un percorso di inizio, manualmente o utilizzando il selettore.

         * **Query di ricerca** Consente di inserire una query di ricerca sotto forma di testo normale.
      * **Opzioni di ricerca avanzata**

         * **Notazione predicato QueryBuilder** Consente di inserire una query di ricerca utilizzando la notazione del predicato QueryBuilder. Ad esempio, è possibile inserire “fulltext=Marketing” per visualizzare nel Carosello tutte le pagine il cui contenuto include “Marketing”. Consulta [API di QueryBuilder](/help/sites-developing/querybuilder-api.md) per una descrizione approfondita delle espressioni di query e per altri esempi.
   * **Ordina per**
Seleziona 
`jcr:title`, `jcr:created`, `cq:lastModified`oppure `cq:template` dal menu a discesa .

   * **Limite** Il numero massimo di voci da utilizzare nel Carosello, facoltativo.





>[!NOTE]
>
>Puoi creare un componente Carosello personalizzato per Adobe Experience Manager, per la visualizzazione delle risorse digitali presenti in DAM AEM. Per ulteriori informazioni, consulta [Creazione di componenti Carosello personalizzati per Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/custom-carousel-components.html).

### Grafico {#chart}

Il componente Grafico consente di aggiungere un grafico a barre, a linee o a torta. AEM crea un grafico a partire dai dati forniti. I dati vengono specificati digitando direttamente nella scheda Dati, o copiando e incollando un foglio di calcolo.

* **Dati**

   * **Dati grafico**
Immetti i dati del grafico in formato CSV; il formato Valori separati da virgola utilizza virgole (&quot;,&quot;) come separatore di campo.

* **Avanzate**

   * **Tipo di grafico** Seleziona un’opzione tra Grafico a torta, Grafico a linee e Grafico a barre.

   * **Testo alternativo** Testo alternativo che viene visualizzato al posto del grafico.

   * **Larghezza** Larghezza del grafico in pixel.

   * **Altezza** Altezza del grafico in pixel.

L’esempio seguente mostra un esempio di dati del grafico, seguiti dal grafico a barre risultante:

![chlimage_1-6](assets/chlimage_1-6.png) ![dc_graph_use](assets/dc_chart_use.png)

>[!NOTE]
>
>Puoi creare un controllo per grafici AEM personalizzato per la visualizzazione di dati presenti in AEM JCR. Per ulteriori informazioni, consulta [Visualizzazione di dati di Adobe Experience Manager in un grafico](https://helpx.adobe.com/experience-manager/using/displaying-experience-manager-data-chart.html).

### Frammenti di contenuto {#content-fragment}

>[!CAUTION]
>
>La funzionalità completa di gestione dei frammenti di contenuto è disponibile solo nell’interfaccia touch.
>
>Il componente Frammento di contenuto è visibile anche nella barra laterale dell’interfaccia classica, ma senza ulteriori funzioni.

I [frammenti di contenuto](/help/sites-classic-ui-authoring/classic-page-author-content-fragments.md) vengono creati e gestiti come risorse indipendenti dalla pagina. Puoi quindi utilizzare questi frammenti, con le relative varianti, durante l’authoring di pagine di contenuto.

### Importazione progettazione {#design-importer}

Questo consente di caricare un file zip che include un pacchetto di progettazione.

### Scarica {#download}

Il componente Scarica crea un collegamento nella pagina web selezionata per scaricare un file specifico. Puoi trascinare un contenuto da Content Finder oppure caricare un file.

* **Download**

   * **Descrizione** Breve descrizione visualizzata con il collegamento per il download.

   * **File** File disponibile per il download nella pagina Web risultante. Trascina una risorsa da Content Finder o fai clic nell’area per caricare il file da rendere disponibile come download.

Nell’esempio di seguito viene illustrato il componente Scarica di Geometrixx:

![dc_download_use](assets/dc_download_use.png)

### Esterno {#external}

Il componente per l’integrazione con applicazioni esterne (**Esterno**) consente di integrare applicazioni esterne nella pagina AEM tramite un iframe.

* **Esterno**

   * **Applicazione di destinazione**

      Specificate l’URL dell’applicazione Web da integrare, ad esempio:

      ```
      https://en.wikipedia.org/wiki/Main_Page
      ```

   * **Passa parametri**

      Se necessario, selezionate la casella per i parametri da passare all’applicazione.

   * **Larghezza e altezza**

      Definite la dimensione dell’iframe.

L’applicazione esterna viene integrata nel sistema paragrafo della pagina AEM, ad esempio, quando si utilizza un’applicazione di destinazione `https://en.wikipedia.org/wiki/Main_Page`:

![chlimage_1-7](assets/chlimage_1-7.png)

>[!NOTE]
>
>A seconda del caso d’uso, per l’integrazione di applicazioni esterne possono essere disponibili altre opzioni, ad esempio l’[Integrazione di portlet](/help/sites-administering/aem-as-portal.md).

### Flash {#flash}

Il componente Flash permette di caricare un filmato Flash. Puoi trascinare una risorsa Flash da Content Finder sul componente oppure usare la finestra di dialogo:

* **Flash**

   * **Filmato Flash**

      File del filmato Flash. Potete trascinare un contenuto da Content Finder oppure fare clic per aprire un finestra con cui individuare il contenuto.

   * **Dimensione**

      Dimensioni in pixel dell’area di visualizzazione destinata al filmato.

* **Immagine alternativa**

   Immagine alternativa da mostrare

* **Avanzate**

   * **Menu di scelta rapida**

      Indica se il menu di scelta rapida deve essere mostrato o nascosto.

   * **Modalità finestra**

      Aspetto della finestra, ad esempio opaca, trasparente o distinta (solida).

   * **Colore sfondo**

      Colore di sfondo selezionato dalla tavola colori fornita.

   * **Versione minima**

      Versione minima di Adobe Flash Player necessaria per riprodurre il filmato. Il valore predefinito è 9.0.0.

   * **Attributi**

      Eventuali altri attributi richiesti.

### Immagine {#image}

Il componente Immagine visualizza un’immagine e il relativo testo in base ai parametri specificati.

Puoi caricare un’immagine, quindi modificarla e manipolarla, ad esempio ritagliandola, ruotandola o aggiungendo un collegamento, un titolo o un testo.

Puoi trascinare un’immagine da [Content Finder](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder) direttamente sul componente o nella relativa finestra di dialogo di modifica. È anche possibile fare doppio clic nell’area centrale della finestra di dialogo di modifica per sfogliare il file system locale e caricare un’immagine. Le due schede della finestra di dialogo Modifica controllano anche tutte le definizioni e le operazioni di alterazione delle immagini:

![dc_image](assets/dc_image.png)

>[!NOTE]
>
>In Internet Explorer non è possibile monitorare l’avanzamento del caricamento.
>
>Se si utilizza Internet Explorer è necessario caricare l’immagine e fare clic su **OK**, quindi riaprire l’immagine per vedere il file caricato nell’anteprima e per eseguire eventuali modifiche (ad es. ritagliare l’immagine).
>
>Consulta la sezione [Piattaforme certificate](/help/release-notes/release-notes.md#certifiedplatforms) per ulteriori informazioni sulle funzioni di HTML5 utilizzate da AEM.

Quando carichi un’immagine, puoi configurare le opzioni seguenti:

* **Mappa**

   Per mappare un’immagine, seleziona Mappa. È possibile specificare come si desidera creare la mappa immagine (rettangolare, poligonale e così via) e la destinazione dell’area.

* **Ritaglia**

   Selezionate Ritaglia per ritagliare un’immagine. Ritagliate l’immagine utilizzando il mouse.

* **Ruota**

   Per ruotare un’immagine, selezionate Ruota. Utilizzare ripetutamente finché l&#39;immagine non viene ruotata nel modo desiderato.

* **Cancella**

   Rimuove l’immagine corrente.

* **Barra Zoom**

   Per ingrandire e ridurre l’immagine, utilizzate la barra di scorrimento al di sotto dell’immagine (sopra ai pulsanti OK e Annulla)

* **Titolo**

   Titolo dell’immagine.

* **Testo alt**

   Testo alternativo da utilizzare per la creazione di contenuto accessibile.

* **Collega a**

   Crea un collegamento a risorse o altre pagine all’interno del sito web.

* **Descrizione**

   Descrizione dell’immagine.

* **Dimensione**

   Imposta l’altezza e la larghezza dell’immagine.

L’immagine finale (con **Titolo** e **Descrizione**) può essere visualizzata come:

![chlimage_1-8](assets/chlimage_1-8.png)

### Contenitore di layout {#layout-container}

>[!CAUTION]
>
>Il componente Contenitore di layout è disponibile anche nell’interfaccia classica, ma le sue funzionalità complete sono disponibili solo nell’interfaccia touch. Per ulteriori informazioni, consulta [Layout reattivo](/help/sites-classic-ui-authoring/classic-page-author-responsive-layout.md).

### Elenco {#list}

Il componente Elenco permette di configurare criteri di ricerca per la creazione di un elenco:

* **Elenco**

   * **Genera elenco con**

      Qui si specifica la provenienza del contenuto dell’elenco. Sono disponibili diversi metodi:

   * A seconda dell’elemento scelto sarà visualizzato un nuovo pannello:

      * **Opzioni per le pagine secondarie**

         * **Elemento secondario di**(pagina padre) Consente di specificare il percorso manualmente o utilizzando il selettore. Non specificare nulla per utilizzare la pagina corrente.
      * **Opzioni per elenco fisso**

         * **Pagine**

            Seleziona un elenco di pagine. Utilizza + per aggiungere altre voci e i pulsanti su/giù per regolare l’ordine.
      * **Opzioni per la ricerca**

         * **Inizia in**

            Immettere un percorso iniziale, manualmente o utilizzando il selettore.

         * **Query di ricerca**

            È possibile immettere una query di ricerca con testo normale.
      * **Opzioni di ricerca avanzata**

         * **Notazione predicato Querybuilder**

            È possibile inserire una query di ricerca utilizzando la notazione predicato Querybuilder. Ad esempio, puoi inserire &quot;fulltext=Marketing&quot; per visualizzare nel carosello tutte le pagine con &quot;Marketing&quot; nel contenuto.

            Vedi [API di QueryBuilder](/help/sites-developing/querybuilder-api.md) per una discussione completa delle espressioni di query e ulteriori esempi.
      * **Tag**

         Specifica la **Pagina padre**, **Tag/Parole chiave** e i criteri di corrispondenza richiesti.
   * **Visualizza come**

      Come devono essere elencati gli elementi: come Collegamenti, Teaser o Notizie.

   * **Ordina per**

      Indica se l’elenco deve essere ordinato e, in tal caso, quale criterio di ordinamento usare. È possibile specificare un criterio o selezionarne uno dall’elenco a discesa fornito.

   * **Limite**

      Specificate il numero massimo di elementi da visualizzare nell’elenco.

   * **Abilita feed**

      Indica se attivare un feed RSS per l’elenco.

   * **Paginare dopo**

      Qui si può specificare quante voci elenco devono essere visualizzate alla volta. Se un elenco contiene più voci di quanto specificato, l’elenco verrà visualizzato in più parti.






Nell’esempio seguente, un componente **Elenco** visualizza una serie di pagine figlie, in base alle definizioni CSS personalizzate della progettazione di un sito.

![dc_list_use](assets/dc_list_use.png)

### Accesso {#login}

Forniscono i campi nome utente e password.

![chlimage_1-9](assets/chlimage_1-9.png)

Puoi configurare i parametri seguenti:

* Accesso

   * Etichetta sezione

      Testo iniziale per i campi di input.

   * Etichetta nome utente

      Testo per etichettare il campo del nome utente.

   * Etichetta password

      Testo per etichettare il campo password.

   * Etichetta pulsante Accesso

      Testo del pulsante di accesso.

   * Reindirizza a

      Puoi specificare la pagina del sito web che deve essere aperta dopo l’accesso dell’utente.

* Accesso già effettuato

   * Etichetta pulsante Continua

      Testo per indicare che l’utente ha già effettuato l’accesso.

### Stato dell’ordine {#order-status}

* **Titolo**

   * **Titolo**

      Specificare il testo del titolo che si desidera visualizzare.

   * **Collegamento**

      Specifica la pagina (prodotto) per la quale deve essere visualizzato lo stato dell’ordine.

   * **Tipo/Dimensione**

      Seleziona dalla selezione fornita.

![chlimage_1-10](assets/chlimage_1-10.png)

### Riferimento {#reference}

Il componente **Riferimento** consente di fare riferimento al testo da un’altra pagina del sito Web AEM (all’interno dell’istanza corrente). Il contenuto del paragrafo a cui viene fatto riferimento verrà visualizzato come se si trovasse nella pagina corrente. Il contenuto verrà aggiornato al modificarsi del paragrafo di origine (potrebbe essere necessario un aggiornamento della pagina).

* **Riferimento paragrafo**

   * **Riferimento**

      Specifica il percorso della pagina e il paragrafo a cui fare riferimento (includere il contenuto).

Per specificare il percorso di un paragrafo è necessario aggiungere in coda al percorso (della pagina) quanto segue:

`.../jcr:content/par/<paragraph-ID>`

Esempio:

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par/similar-products`

Oltre a fare riferimento a un paragrafo specifico, il percorso può essere modificato anche in modo da specificare un sistema paragrafo completo. Questa operazione può essere eseguita inserendo in coda al percorso quanto segue:

`/jcr:content/par`

Esempio:

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par`

Una volta configurato il contenuto apparirà esattamente come nella pagina sorgente. Il fatto che si tratti di un riferimento è visibile solo quando il componente viene aperto per la modifica:

![chlimage_1-11](assets/chlimage_1-11.png)

### Ricerca {#searching}

Il componente Ricerca aggiunge alla pagina le funzionalità di ricerca.

Puoi configurare i parametri seguenti:

* Ricerca

   * **Tipi di nodo**

      Se la ricerca deve essere limitata a specifici tipi di nodo elencali qui; ad esempio, `cq:Page`.

   * **Percorso di ricerca**

      Specificare la pagina principale del ramo che si desidera cercare.

   * **Testo pulsante Cerca**

      Nome visualizzato sul pulsante di ricerca.

   * **Testo per statistiche**

      Testo visualizzato sopra i risultati di ricerca.

   * **Testo Nessun risultato**

      Se non vi sono risultati, viene visualizzato il testo inserito qui.

   * **Controllo ortografia del testo**

      Se un utente inserisce un termine simile, prima del termine viene visualizzato questo testo.
Ad esempio, se digitate geometrixxe, il sistema visualizza &quot;Intendete? geometrixx&quot;.

   * **Testo per pagini simili**

      Testo visualizzato accanto a un risultato per pagine simili. Fate clic su questo collegamento per vedere altre pagine con contenuti simili.

   * **Testo di ricerche correlate**

      Testo visualizzato accanto a ricerche per termini e argomenti correlati.

   * **Testo di tendenze ricerca**

      Titolo al di sopra dei termini di ricerca inseriti dall’utente.

   * **Etichetta pagina risultati**

      Testo visualizzato in fondo all’elenco, con collegamenti verso le altre pagine di risultati.

   * **Etichetta precedente**

      Nome visualizzato sul collegamento verso le pagine di ricerca precedenti.

   * **Etichetta successiva**

      Nome visualizzato sul collegamento verso le pagine di ricerca successive.

L’esempio seguente mostra il componente Ricerca dopo la ricerca della parola *geometrixx* dalla directory principale di un’installazione standard. L’esempio mostra anche l’impaginazione dei risultati:

![dc_search_use](assets/dc_search_use.png)

L’esempio seguente mostra un termine di ricerca con errore ortografico e non disponibile:

![dc_search_usenotfound](assets/dc_search_usenotfound.png)

### Sitemap {#sitemap}

Un elenco automatico di tipo sitemap, con impostazioni predefinite, include tutte le pagine, (sotto forma di collegamenti attivi), presenti nel sito Web corrente. Ad esempio, un estratto mostra quanto segue:

![dc_sitemap_use](assets/dc_sitemap_use.png)

Se necessario è possibile configurare:

* **Sitemap**

   * **Percorso directory principale**

      Percorso di inizio per la creazione dell’elenco.

### Slideshow {#slideshow}

Questo componente permette di caricare una serie di immagini da visualizzare sulla pagina sotto forma di slideshow. Puoi aggiungere o rimuovere immagini e assegnare un titolo a ognuna di esse. In Avanzate è inoltre possibile specificare la dimensione dell’area di visualizzazione.

Puoi configurare i parametri seguenti:

* **Diapositive**

   * **Nuova diapositiva**

      È possibile specificare una selezione di diapositive utilizzando **Aggiungi** e **Rimuovi**).

   * **Titolo**

      Se necessario, specifica un titolo. Questo viene sovrapposto sulla diapositiva appropriata.

* **Avanzate**

   * **Dimensione**

      Specifica la larghezza e l’altezza in pixel.

Quindi, il componente Presentazione visualizza in sequenza ciascuna immagine per un breve lasso di tempo, prima di passare alla diapositiva successiva con un effetto di dissolvenza:

![dc_slideshow_use](assets/dc_slideshow_use.png)

### Tabella {#table}

>[!NOTE]
>
>Il componente **Tabella** è basato sull’[editor Rich Text](/help/sites-classic-ui-authoring/classic-page-author-rich-text-editor.md), come il componente **[Testo](#text)**.
>
>Si consiglia di utilizzare il componente **Tabella** per le tabelle, anche se è possibile generarle con il componente **Testo**.

Il componente **Tabella** è preconfigurato per consentire di generare, compilare e formattare una tabella. Utilizzando la finestra di dialogo puoi configurare la tabella e creare contenuti:

* da zero
* copiando e incollando un foglio di calcolo o una tabella da un programma di modifica esterno (come Excel, OpenOffice, Notepad e così via).

![dc_table](assets/dc_table.png)

La schermata seguente mostra un esempio del componente Tabella; la progettazione è determinata dal CSS specifico per il sito:

![dc_table_use](assets/dc_table_use.png)

### Tag cloud {#tag-cloud}

Una tag cloud mostra una rappresentazione grafica di una selezione di tag associati al contenuto del sito Web:

![dc_tagclouduse](assets/dc_tagclouduse.png)

Per la configurazione del componente Tag cloud, puoi specificare:

* **Tag da visualizzare** La posizione di origine dei tag da visualizzare. Puoi eseguire la selezione da una pagina o da una pagina con tutte le relative pagine figlie oppure tutti i tag.

* **Pagina** La pagina alla quale verrà fatto riferimento.

* **Nessun collegamento sui tag** Consente di specificare se i tag visualizzati devono fungere da collegamenti oppure no.

Per ulteriori informazioni sull’applicazione dei tag, consulta [Utilizzo dei tag](/help/sites-classic-ui-authoring/classic-feature-tags.md).

### Testo {#text}

>[!NOTE]
>
>Il componente **Testo** è basato sull’[editor RTF](/help/sites-classic-ui-authoring/classic-page-author-rich-text-editor.md), come il componente **[Tabella](#table)**.
>
>Si consiglia di utilizzare il componente **Tabella** per le tabelle, anche se è possibile generarle con il componente **Testo**.

Il componente Testo consente di inserire un blocco di testo utilizzando un editor WYSIWYG, le cui funzionalità sono fornite dall’[Editor Rich Text](/help/sites-classic-ui-authoring/classic-page-author-rich-text-editor.md). Sono disponibili varie icone che consentono di formattare il testo, specificando caratteristiche del font, allineamento, collegamenti, elenchi e rientri.

![dc_text](assets/dc_text.png)

La scheda **Stili** della finestra di dialogo **Modifica** consente di impostare anche:

* **Spaziatore**
* **Stile di testo**

Il testo formattato verrà quindi visualizzato sulla pagina; la progettazione effettiva dipenderà dal sito CSS:

![dc_text_use](assets/dc_text_use.png)

Per informazioni più dettagliate sul componente Testo e sulla funzionalità fornita dall’editor Rich Text, consulta la pagina [editor Rich Text](/help/sites-classic-ui-authoring/classic-page-author-rich-text-editor.md).

#### Modifica locale {#inplace-editing}

Oltre alla modalità di modifica del testo RTF basata su finestra di dialogo, AEM supporta anche la [modifica locale](/help/sites-authoring/editing-content.md), che consente di modificare direttamente il testo, così come viene visualizzato nel layout della pagina.

### Testo e immagine {#text-image}

Il componente Testo e immagine aggiunge un blocco di testo e un’immagine. È inoltre possibile aggiungere testo e immagini separatamente; per maggiori dettagli, vedi i componenti [Testo](#text) e [Immagine](#image).

![chlimage_1-12](assets/chlimage_1-12.png) ![chlimage_1-13](assets/chlimage_1-13.png)

Puoi configurare i parametri seguenti:

* **Stili dei componenti** (**Stili**)

   Qui è possibile specificare l’allineamento a sinistra o a destra dell’immagine. L’impostazione predefinita prevede l’allineamento dell’immagine a **Sinistra**.

* **Proprietà immagine** (**Proprietà immagine avanzate**)

   Potete specificare i seguenti parametri:

   * **Risorsa immagine**

      Carica l’immagine richiesta.

   * **Titolo**

      Titolo del blocco di testo, che verrà visualizzato al passaggio del mouse.

   * **Testo alt**

      Testo alternativo che verrà mostrato qualora l’immagine non sia disponibile. Se questo campo viene lasciato vuoto, verrà utilizzato il titolo.

   * **Collega a**

      Specifica un percorso di destinazione.

   * **Descrizione**

      Descrizione dell’immagine.

   * **Dimensione**

      Imposta l’altezza e la larghezza dell’immagine.

L’esempio seguente mostra un componente Testo e immagine che mostra l’immagine allineata a sinistra:

![dc_textimage_use](assets/dc_textimage_use.png)

### Titolo {#title}

Il componente Titolo può visualizzare uno dei seguenti elementi:

* il nome della pagina corrente, qualora il campo Titolo venga lasciato vuoto; oppure
* il testo specificato nel campo Titolo.

Puoi configurare i parametri seguenti:

* **Titolo**

   Per usare un nome diverso dal titolo della pagina, inseritelo in questo campo.

* **Collegamento**

   URI, qualora il titolo debba fungere da collegamento.

* **Tipo/Dimensione**

   Selezionate Piccolo o Grande dall’elenco a discesa. Con Piccolo viene generato come immagine. Con Grande viene generato come testo.

L’esempio seguente mostra un componente **Titolo** visualizzato in base al CSS specifico del sito.

![dc_title_use](assets/dc_title_use.png)

### Video {#video}

Il componente **Video** consente di inserire un elemento video predefinito, disponibile out-of-the-box, nella pagina.

Per informazioni sull’uso con gli elementi HTML5, consulta anche [Configurare i profili video](/help/sites-administering/config-video.md#configuringvideoprofiles).

Dopo aver posizionato un’istanza del componente sulla pagina puoi configurare i parametri seguenti:

* Video

   * **Risorsa video**

      Carica o rilascia la risorsa video.

   * **Dimensione**

      Le dimensioni native del video (larghezza x altezza, in pixel) vengono riportate nelle caselle accanto a Dimensione (ved. sopra). Per escludere le dimensioni native del video, potete inserire manualmente nuovi valori di larghezza e altezza. Fai clic su **OK** per chiudere la finestra di dialogo.

>[!NOTE]
>
>Tra i formati supportati:
>
>* `.mp4`
>* `Ogg`
>* `FLV` (video Flash)
>


## Colonne {#columns}

Le colonne sono un meccanismo per controllare il layout del contenuto in AEM. In un’installazione standard sono inclusi componenti per la creazione di due e/o 3 colonne.

L’esempio seguente illustra l’utilizzo dei componenti 2 Colonne e 3 Colonne. Per nuovi componenti puoi utilizzare i segnaposto:

![chlimage_1-14](assets/chlimage_1-14.png)

### 2 Colonne {#columns-1}

Componente Controllo colonna con impostazione predefinita di 2 colonne uguali.

### 3 Colonne {#columns-2}

Componente Controllo colonna con impostazione predefinita di 3 colonne uguali.

### Controllo colonna {#column-control}

Il componente Controllo colonna consente agli utenti di selezionare la modalità di suddivisione del contenuto del pannello principale della pagina web in più colonne. Gli utenti possono selezionare il numero di colonne richiesto (da un elenco predefinito) e quindi creare, eliminare o spostare i contenuti all’interno di ciascuna colonna.

* **Controllo colonna**

   * **Layout colonna**

      Selezionate il numero di colonne desiderato. Una volta creata, ogni colonna dispone di un proprio collegamento per trascinare componenti o risorse durante l’aggiunta di contenuto.

## Modulo {#form}

I componenti Modulo permettono di creare dei moduli che i visitatori possono compilare e inviare. I moduli e i componenti modulo consentono di raccogliere informazioni come ad esempio feedback dagli utenti (ad es. mediante un modulo di valutazione del livello di soddisfazione) e informazioni (ad es. mediante un modulo di registrazione utente).

>[!NOTE]
>
>Consulta [Aiuto moduli AEM](/help/forms/home.md) per informazioni sui moduli AEM.

I moduli sono composti di diversi componenti distinti:

* **Modulo**

   Il componente Modulo definisce l’inizio e la fine di un nuovo modulo sulla pagina. È possibile quindi inserire altri componenti tra tali elementi, ad esempio tabelle, file da scaricare e così via.

* **Campi ed elementi per moduli**

   I campi e gli elementi per i moduli possono comprendere caselle di testo, pulsanti di scelta, immagini e così via. L’utente spesso completa un’azione in un campo modulo, ad esempio digita del testo. Per ulteriori informazioni, consultate le sezioni dedicate ai singoli elementi.

* **Componenti Profilo**

   I componenti Profilo si riferiscono ai profili dei visitatori utilizzati per collaborazione di tipo social network e altre aree in cui è richiesta una personalizzazione in base al visitatore.

Di seguito è visualizzato un modulo di esempio, composto dal componente **Modulo** (inizio e fine), con due campi **di testo** **modulo** per consentire l’input da parte del visitatore, un campo di **testo** **generale** utilizzato per il testo lead-in e un pulsante **Invia**.

![dc_form](assets/dc_form.png)

>[!NOTE]
>
>Informazioni sullo sviluppo e sulla personalizzazione ulteriori del moduli sono disponibili sulla [pagina Sviluppo di moduli](/help/sites-developing/developing-forms.md). Sono inclusi, tra gli altri, aggiunta di azioni, vincoli, precaricamento di campi e utilizzo di script per richiamare un servizio per l’esecuzione di un’azione.

### Impostazioni comuni a numerosi componenti modulo {#settings-common-to-many-form-components}

Anche se i vari componenti modulo hanno funzioni diverse, molti di essi offrono opzioni e parametri simili.

Quando si configura un componente modulo, la finestra di dialogo presenta le seguenti schede:

* **Titolo e testo**

   Qui si specificano le informazioni di base, ad esempio il titolo del modulo ed eventuale testo di corredo. Se appropriato è inoltre possibile definire informazioni chiave, ad esempio se il campo consente una selezione multipla e quali voci possono essere selezionate.

* **Valori iniziali**

   Consente di specificare un valore predefinito.

* **Vincoli**

   Qui si specifica se un campo è obbligatorio ed eventuali vincoli associati al campo (ad es. se il valore deve essere numerico e così via).

* **Attribuzione stile**

   Indica la dimensione e lo stile dei campi.

>[!NOTE]
>
>I campi disponibili variano notevolmente in base al singolo componente.

Queste schede forniscono i parametri necessari, che dipendono dal tipo di componente, ma possono includere:

* **Titolo e testo**

   * **Nome elemento**

      Nome dell’elemento modulo. Indica dove vengono registrati i dati nella directory archivio.
Questo campo è obbligatorio e può contenere solo i seguenti caratteri:

      * caratteri alfanumerici
      * `_ . / : -`
   * **Titolo**

      Titolo da visualizzare con il campo. Se lasciato vuoto, viene visualizzato il titolo predefinito.

   * **Descrizione**

      Consente di fornire eventuali informazioni aggiuntive per l’utente. Nel modulo questo viene visualizzato sotto il campo, in un font di dimensioni più piccole rispetto al titolo.

   * **Mostra/Nascondi**

      Determina quando il campo deve essere visibile.


* **Valori iniziali**

   * **Valore predefinito**

      Il valore visualizzato nel campo all’apertura del modulo, ossia prima che venga compilato dall’utente.

* **Vincoli**

   * **Obbligatorio**

      Questo dipende dal tipo di componente modulo, ma fornisce una o più caselle di controllo per indicare che questo campo, o alcune parti di esso, sono obbligatorie.

   * **Messaggio richiesto**

      Un messaggio per informare gli utenti che questo campo è obbligatorio; anche un campo obbligatorio sarà contrassegnato da un asterisco.

   * **Vincolo**

      I vincoli disponibili per la selezione dipendono dal tipo di componente modulo.

   * **Messaggio vincolo**

      Un messaggio per informare gli utenti di ciò che è necessario.

* **Attribuzione stile**

   * **Dimensione**

      In righe e colonne.

   * **Larghezza**

      In pixel.

   * **CSS**

### Modulo (componente) {#form-component}

Il componente Modulo definisce l’inizio e la fine di un modulo con gli elementi **Inizio modulo** e **Fine modulo**. Questi sono sempre utilizzati in coppia per garantire la corretta definizione del modulo.

![dc_form-1](assets/dc_form-1.png)

Tra l’inizio e la fine di un modulo puoi aggiungere componenti modulo che definiscono i campi di immissione presentati agli utenti.

#### Inizio del modulo {#start-of-form}

Questo componente è necessario per definire l’inizio di un nuovo modulo su una pagina. Puoi configurare i parametri seguenti:

* **Modulo**

   * **Pagina di ringraziamento**

      La pagina a cui passare per ringraziare i visitatori dopo l’invio del modulo. Se viene lasciato vuoto, dopo l’invio viene di nuovo visualizzato il modulo.

   * **Avvia flusso di lavoro**

      Determina il flusso di lavoro che viene attivato dopo l’invio del modulo.

* **Avanzate**

   * **Tipo di azione**

      Un modulo richiede un’azione che definisca l’operazione da avviare con i dati inviati dall’utente (simile a action= in HTML). Alcuni hanno bisogno di **Configurazione azione**.

      Una selezione di tipi di azioni è inclusa in un’installazione standard AEM:

      * **Richiesta account**
      * **Crea contenuto**
      * **Crea lead**
      * **Crea e aggiorna account**
      * **Servizio e-mail: crea utente con sottoscrizione e aggiungi all&#39;elenco**
      * **Servizio e-mail: invia e-mail di risposta automatica**
      * **Servizio e-mail: annulla sottoscrizione a mailing list**
      * **Modifica Community**
      * **Modifica risorse**
      * **Modifica risorse controllate da flusso di lavoro**
      * **Mail**
      * **Dettagli ordine inoltrato**
      * **Aggiornamento profilo**
      * **Ripristina password**
      * **Imposta password**
      * **Contenuto store**

         Tipo di azione predefinito.

      * **Contenuto store con caricamenti**
      * **Invia ordine**
      * **Annulla sottoscrizione utente**
      * **Aggiorna ordine**
   * **Identificatore modulo**

      L’identificatore del modulo identifica il modulo in maniera univoca. Utilizza l’identificatore del modulo se sono presenti diversi moduli su una stessa pagina, avendo cura di utilizzare identificatori diversi per ciascun modulo.

   * **Percorso di caricamento**

      Percorso delle proprietà nodo utilizzato per caricare valori predefiniti nei campi del modulo.
Si tratta di un campo facoltativo, per specificare il percorso di un nodo nella directory archivio. Quando alcune proprietà di questo nodo corrispondono ai nomi dei campi, i relativi campi del modulo vengono precompilati con il valore della proprietà corrispondente. In assenza di proprietà corrispondenti, il campo contiene il valore predefinito.
Utilizzando **Percorso di caricamento** potete precaricare il modulo con valori inseriti nei campi necessari. Vedi [Precaricamento dei valori dei moduli](/help/sites-developing/developing-forms.md#preloading-form-values).

   * **Convalida client**

      Indica se il modulo richiede la convalida client (la convalida server viene *sempre* effettuata). Questa può essere effettuata in combinazione con il componente per moduli **Captcha**.

   * **Tipo risorsa validazione**

      Definisce il tipo di risorsa per la convalida del modulo se si desidera convalidare l’intero modulo (invece dei singoli campi). Se si convalida l’intero modulo, occorre includere anche uno dei seguenti elementi:

      * Uno script per la convalida client:

         `/apps/<myApp>/form/<myValidation>/formclientvalidation.jsp`

      * Uno script per la convalida lato server:

         `/apps/<myApp>/form/<myValidation>/formservervalidation.jsp`
   * **Configurazione azione**

      Le opzioni disponibili in **Configurazione azione** dipendono dal **Tipo di azione** selezionato:

      * **Richiesta account**

         * **Pagina di creazione account** Pagina utilizzata per la creazione di un nuovo account.
      * **Crea contenuto**

         * Percorso del contenuto Il percorso del contenuto riprodotto dal modulo. Immettere un percorso che termina con una barra `/`. La barra indica che per ogni porta del modulo viene creato un nuovo nodo nel percorso specificato; ad esempio:
            `/forms/feedback/`

         * **Tipo**

            Seleziona il tipo richiesto.

         * **Modulo**

            Specificare il modulo.

         * **Rendering con**

            Seleziona l’opzione desiderata dall’elenco.

         * **Tipo risorsa**

            Se impostato, questo viene aggiunto a ogni commento come `sling:resourceType`

         * **Selettore vista**
      * **Crea lead**

         * **Il lead verrà aggiunto a questo elenco** Consente di specificare l’elenco di lead richiesto.
      * **Crea e aggiorna account**

         * **Gruppo iniziale**

            Gruppo a cui assegnare l’utente.

         * **Pagina principale**

            Pagina da visualizzare dopo l’accesso.

         * **Percorso**

            Percorso (relativo) per la creazione e memorizzazione del nuovo account.

         * **Visualizza dati...**

            Fate clic su questo pulsante per accedere a informazioni sui risultati del modulo in Bulk Editor. Da qui puoi esportare le informazioni in un `.tsv` File (separato da tabulazioni) da utilizzare, ad esempio, in un foglio di calcolo Excel.
      * **Mail**

         * **Da**

            Inserire l’indirizzo e-mail dal quale deve essere inviato il messaggio e-mail.

         * **Invia a**

            Inserite gli indirizzi e-mail a cui deve essere inviato il modulo.

         * **CC**

            Inserite gli indirizzi e-mail per invio CC.

         * **CCN**

            Inserite gli indirizzi e-mail per invio CCn.

         * **Oggetto**

            Inserite l’oggetto del messaggio e-mail.
      * **Ripristina password**

         * **Pagina modifica password**

            Pagina utilizzata per modificare la password.
      * **Contenuto store**

         * **Percorso contenuto**

            Percorso di eventuale contenuto riprodotto nel modulo. Inserite un percorso che termina con una barra `/`. La barra indica che per ciascuna porta modulo viene creato un nuovo nodo nel percorso indicato, ad esempio:
            `/forms/feedback/`

         * **Visualizza dati...**

            Fate clic su questo pulsante per accedere a informazioni sui risultati del modulo in Bulk Editor. Da qui è possibile esportare le informazioni in un file .tsv (separato da tab) da utilizzare, ad esempio, in un foglio di calcolo Excel).
      * **Contenuto store con caricamenti**

         Ha le stesse opzioni di **Contenuto store**.

      * **Annulla sottoscrizione utente**

         * **Il lead verrà eliminato da questo elenco**

            Specifica l’elenco di lead richiesto.










#### Fine del modulo {#end-of-form}

Questo indica la fine del modulo. È possibile configurare quanto segue:

* **Fine modulo**

   * **Mostra pulsante Invia**

      Indica se mostrare o meno un pulsante Invia.

   * **Nome invio**

      Identificatore, qualora il modulo contenga più pulsanti Invia.

   * **Titolo invio**

      Nome visualizzato sul pulsante, ad esempio Invia.

   * **Mostra pulsante Ripristina**

      Selezionate la casella per rendere visibile il pulsante Ripristina.

   * **Ripristina titolo**

      Nome visualizzato sul pulsante Ripristina.

   * **Descrizione**

      Informazioni riportate sotto il pulsante.

### Nome account {#account-name}

Consente di inserire un nome account:

![dc_form_account_name](assets/dc_form_accountname.png)

### Indirizzo {#address}

Consente di inserire un campo di indirizzo internazionale nel seguente formato:

![dc_form_addressfield](assets/dc_form_addressfield.png)

Il componente è configurato per l’utilizzo immediato, ma puoi modificare la configurazione se necessario. Ad esempio, possono essere aggiunti vincoli per i singoli elementi dell’indirizzo. Lasciando i campi vuoti saranno utilizzate le impostazioni predefinite.

### Captcha {#captcha}

Il componente Captcha richiede all’utente di inserire la stringa alfanumerica visualizzata sullo schermo. Con ogni aggiornamento della schermata viene visualizzata una stringa diversa.

![dc_form_captcha](assets/dc_form_captcha.png)

Puoi configurare vari parametri per questo componente, incluso un messaggio da visualizzare se la stringa Captcha non è valida.

### Gruppo di caselle di selezione {#checkbox-group}

Una casella di selezione consente di generare un elenco composto di una o più caselle. L’utente potrà selezionare più caselle.

![dc_form_checkboxgroupuse](assets/dc_form_checkboxgroupuse.png)

Puoi specificare vari parametri, inclusi un titolo, una descrizione e il nome dell’elemento. Utilizza i pulsanti + e - per aggiungere o rimuovere elementi, quindi riposizionali mediante le frecce verso l’alto o il basso.

>[!NOTE]
>
>Utilizzando **Percorso di caricamento elementi** puoi precaricare l’elenco del gruppo di caselle di selezione con i relativi valori.
>
>Consulta [Precaricamento dei campi modulo con più valori](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Dati carta di credito {#credit-card-details}

Questo consente di includere i campi necessari per inserire i dati della carta di credito. Puoi configurarlo per specificare i tipi di carte accettate e le informazioni richieste (ad esempio, il codice protezione).

![chlimage_1-15](assets/chlimage_1-15.png)

### Elenco a discesa {#dropdown-list}

Un elenco a discesa più essere configurato con una serie di valori da selezionare:

![dc_form_dropdownlistuse](assets/dc_form_dropdownlistuse.png)

Puoi specificare un titolo e le voci incluse nell’elenco. Utilizza i pulsanti + e - per aggiungere o rimuovere le voci, quindi riposizionale mediante le frecce verso l’alto o il basso. Puoi specificare se gli utenti sono autorizzati a selezionare più voci dall’elenco e tutte le voci che dovrebbero essere selezionate automaticamente al primo accesso all’elenco (valori iniziali).

>[!NOTE]
>
>Utilizzando **Percorso di caricamento elementi** puoi precaricare nell’elenco a discesa i relativi valori.
>
>Consulta [Precaricamento dei campi modulo con più valori](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Caricamento di file {#file-upload}

Il componente Caricamento file offre all’utente la possibilità di selezionare e caricare un file.

![dc_form_fileupload](assets/dc_form_fileupload.png)

>[!NOTE]
>
>Puoi creare un componente di caricamento personalizzato per caricare i file su un Servlet Sling. Per ulteriori informazioni, consulta [Caricamento dei file in Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/uploading-files-aem1.html).

### Campo nascosto {#hidden-field}

Questo componente consente di creare un campo nascosto. Questi possono essere utilizzati per vari scopi; ad esempio, quando è necessario eseguire un’azione dopo l’invio del modulo, o quando dati nascosti sono necessari in fase di post-elaborazione.

![dc_form_hiddenfield](assets/dc_form_hiddenfield.png)

>[!NOTE]
>
>Puoi inoltre personalizzare il modulo in modo da mostrare o nascondere specifici componenti a seconda dei valori di altri campi nel modulo. La modifica della visibilità di un campo modulo è utile se il campo è richiesto solo in presenza di particolari condizioni.
>
>Consulta [Mostrare e nascondere i componenti di un modulo](/help/sites-developing/developing-forms.md#showing-and-hiding-form-components).

### Pulsante immagine {#image-button}

Un pulsante immagine consente di creare un pulsante con testo e immagine personalizzati:

![dc_form_imagebutton](assets/dc_form_imagebutton.png)

### Caricamento immagine {#image-upload}

Il componente Caricamento immagine offre all’utente la possibilità di selezionare e caricare un file immagine.

![dc_form_imageupload](assets/dc_form_imageupload.png)

### Campo collegamento {#link-field}

Il componente Campo collegamento permette di specificare un URL:

![dc_form_link](assets/dc_form_link.png)

Viene utilizzato frequentemente per il modulo Evento calendario, in cui fornisce un campo URL/collegamento per un evento.

### Campo password {#password-field}

Viene utilizzato per consentire all’utente di inserire la propria password:

![dc_form_password](assets/dc_form_password.png)

### Reimpostazione password {#password-reset}

Questo componente fornisce all’utente due campi:

* per inserire una password
* per inserire nuovamente la password e verificare che sia stata inserita correttamente.

Con le impostazioni predefinite, il componente si presenta come segue:

![dc_password_reset](assets/dc_password_reset.png)

### Gruppo pulsanti di scelta {#radio-group}

Un gruppo pulsanti di scelta offre un elenco composto di uno o più caselle di selezione. L’utente potrà selezionarne solo uno.

Puoi specificare il nome dell’elemento insieme a un titolo e descrizione. Utilizza i pulsanti + e - per aggiungere o rimuovere elementi, quindi riposizionali mediante le frecce verso l’alto o il basso e se necessario specifica un valore predefinito:

![dc_form_radiogroupuse](assets/dc_form_radiogroupuse.png)

>[!NOTE]
>
>Utilizzando **Percorso di caricamento elementi** puoi precaricare il gruppo pulsanti di scelta con i relativi valori.
>
>Consulta [Precaricamento dei campi modulo con più valori](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Pulsante Invia {#submit-button}

Questo componente permette di creare un pulsante Invia, con testo predefinito:

![dc_form_submitbutton](assets/dc_form_submitbutton.png)

oppure con testo personalizzato:

![dc_form_submitbuttonuse](assets/dc_form_submitbuttonuse.png)

### Campo tag {#tags-field}

Questo campo consente di selezionare i tag:

![dc_form_tags_use](assets/dc_form_tags_use.png)

Puoi specificare vari parametri, compresi i namespace utilizzabili mediante la scheda apposita:

* **Campo tag**

   * **Namespace consentiti**

      * **Geometrixx Outdoors**
      * **Flusso di lavoro**
      * **Forum**
      * **Fotografia Stock**
      * **Geometrixx Media**
      * **Tag standard**
      * **Marketing**
      * **Proprietà risorsa**
   * **Larghezza in pixel**
   * **Dimensione popup**


### Campo testo {#text-field}

Il campo di testo standard può essere configurato con la dimensione richiesta e con un messaggio introduttivo personalizzato:

![dc_form_text](assets/dc_form_text.png)

### Pulsanti invio flusso di lavoro {#workflow-submit-button-s}

Questo consente di creare un pulsante Invia da utilizzare in un flusso di lavoro.

![chlimage_1-16](assets/chlimage_1-16.png)
