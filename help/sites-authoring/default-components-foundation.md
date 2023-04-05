---
title: Componenti di base
seo-title: Foundation Components
description: Componenti di base
seo-description: null
uuid: 3caf9123-ae58-4590-af2f-57ef076daf7f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: ea2a523e-8d26-4be4-822f-35f153e40308
docset: aem65
legacypath: /content/docs/en/aem/6-2/author/page-authoring/default-components/editmode
pagetitle: Foundation Components
exl-id: 278701f3-3f0c-45f4-90b7-c0e316a7da8a
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '7200'
ht-degree: 9%

---

# Componenti di base {#foundation-components}

>[!CAUTION]
>
>La maggior parte dei componenti di base è ora obsoleta con AEM 6.5. Vedi [note sulla versione](/help/release-notes/deprecated-removed-features.md) per ulteriori informazioni.
>
>Adobe consiglia di utilizzare i [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) in progetti AEM. Questi componenti fanno parte del [Contenuto di esempio di We.Retail](/help/sites-developing/we-retail.md) e può anche essere [installati separatamente e utilizzati per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html) dall’amministratore.
>
>È possibile utilizzare [AEM suite di strumenti di modernizzazione](https://opensource.adobe.com/aem-modernize-tools/) per eseguire il refactoring del sito basato su componenti di base per utilizzare i componenti core.

I componenti di base sono stati progettati per l’utilizzo durante la creazione di contenuti per una pagina web standard. Costituiscono un sottoinsieme dei componenti disponibili out-of-the-box per un’installazione standard di AEM.

Alcuni sono immediatamente disponibili tramite il browser Componenti. Sono disponibili anche diverse altre utilizzando [modalità di progettazione](/help/sites-authoring/default-components-designmode.md) (se la pagina è basata su un modello statico) o [modifica del modello](/help/sites-authoring/templates.md) (se la pagina è basata su un modello modificabile).

È supportato l’utilizzo di componenti di base, ma per lo più obsoleti e sostituiti dai componenti core, che offrono maggiore estensibilità e flessibilità.

>[!NOTE]
>
>Questa sezione descrive solo i componenti disponibili pronti all’uso in un’installazione AEM standard.
>
>A seconda dell’istanza, è possibile che i componenti personalizzati siano stati sviluppati esplicitamente per le proprie esigenze. Questi componenti personalizzati possono anche avere lo stesso nome di alcuni dei componenti qui descritti.

I componenti sono disponibili nella sezione **Componenti** scheda del pannello laterale dell’Editor pagina quando [modifica di una pagina](/help/sites-authoring/editing-content.md).

Puoi selezionare un componente e trascinarlo nella posizione desiderata sulla pagina. Puoi quindi modificarlo utilizzando:

* [Configura proprietà](/help/sites-authoring/editing-page-properties.md)
* [Modifica contenuto](/help/sites-authoring/editing-content.md)

* [Modifica contenuto - Modalità a tutto schermo](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)

I componenti sono ordinati in base a varie categorie denominate gruppi di componenti, tra cui:

* [Generale](#general): Include componenti di base quali testo, immagini, tabelle e grafici.
* [Colonne](#columns): Include i componenti necessari per organizzare il layout dei contenuti.
* [Modulo](#formgroup): Include tutti i componenti necessari per creare un modulo.

## Generale {#general}

I componenti Generali sono i componenti di base utilizzati per creare contenuti.

### Elemento account {#account-item}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Puoi definire un collegamento con titolo e descrizione.

![chlimage_1-88](assets/chlimage_1-88.png)

### Immagine adattiva {#adaptive-image}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core immagine](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=it) invece.

Il componente Immagine adattiva foundation genera immagini di dimensioni tali da adattarsi alla finestra in cui viene aperta la pagina web. Per utilizzare il componente, fornisci una risorsa immagine dal file system o da DAM. Quando la pagina web viene aperta, il browser scarica una copia dell’immagine che è stata ridimensionata in modo da adattarla alla finestra corrente.

Le dimensioni della finestra possono essere determinate dalle seguenti caratteristiche:

* Schermata del dispositivo: In genere, i dispositivi mobili visualizzano le pagine web in modo che si estendono su tutto lo schermo.
* Dimensioni della finestra del browser Web: Gli utenti di computer portatili e desktop possono ridimensionare le finestre del browser Web.

Ad esempio, il componente genera un’immagine piccola quando la pagina web viene aperta su un cellulare e un’immagine media quando viene aperta su un tablet. Su un laptop, il componente crea e distribuisce un’immagine di grandi dimensioni quando la pagina viene aperta in un browser web con dimensioni massime. Quando il browser viene ridimensionato per adattarsi a una parte dello schermo, il componente si adatta fornendo un’immagine più piccola e aggiorna la visualizzazione.

#### Formati immagine supportati {#supported-image-formats}

Con il componente Immagine adattiva è possibile utilizzare file di immagine con le seguenti estensioni:

* .jpg
* .jpeg
* .png
* .gif &#42;&#42;

>[!CAUTION]
>
>I file GIF animati non sono supportati in AEM per le rappresentazioni adattive.

#### Dimensioni e qualità delle immagini {#images-sizes-and-quality}

Nella tabella seguente sono elencati i valori di larghezza dell&#39;immagine generati per la larghezza di visualizzazione specificata. L’altezza dell’immagine generata viene calcolata in modo da mantenere proporzioni costanti e non si verifica spazio vuoto all’interno del bordo dell’immagine. Il ritaglio può essere utilizzato per evitare spazi bianchi.

Quando l&#39;immagine è un&#39;immagine di JPEG, la dimensione del riquadro di visualizzazione può anche influenzare la qualità di JPEG. Sono possibili le seguenti qualità JPEG:

* Bassa (0,42)
* Media (0,82)
* Alta (1,00)

| **Intervallo di larghezza di visualizzazione (pixel)** | **Larghezza immagine (pixel)** | **Qualità JPEG** | **Tipo di dispositivo di destinazione** |
|---|---|---|---|
| larghezza &lt;= 319 | 320 | bassa |  |
| larghezza = 320 | 320 | media | Telefono cellulare (verticale) |
| 320 &lt; larghezza &lt; 481 | 480 | media | Telefono cellulare (orizzontale) |
| 480 &lt; larghezza &lt; 769 | 476 | alta | Tablet (verticale) |
| 768 &lt; larghezza &lt; 1025 | 620 | alta | Tablet (orizzontale) |
| larghezza &lt;= 1025 | full (dimensione originale) | alta | Desktop |

#### Proprietà {#properties}

La finestra di dialogo consente di modificare le proprietà per l’istanza del componente Immagine adattiva, molte delle quali sono comuni con il componente Immagine su cui è basato. Le proprietà sono disponibili in due schede:

* **Immagine**

   * **Immagine**
Trascina un’immagine da Content Finder oppure fai clic per aprire una finestra con cui caricare un’immagine. Una volta caricata l’immagine, è possibile ritagliarla, ruotarla o eliminarla. Per ingrandire e ridurre l’immagine, utilizzate la barra di scorrimento al di sotto dell’immagine (sopra i pulsanti OK e Annulla)

   * **Ritaglio**
Ritaglia parte di un&#39;immagine. Trascinate il bordo per ritagliare l’immagine.

   * **Ruota**
Fate clic più volte su Ruota fino a ottenere la rotazione desiderata.

   * **Cancella**
Rimuovi l&#39;immagine corrente.

* **Avanzate**

   * **Titolo**
Il componente Immagine adattiva non utilizza questa proprietà.

   * **Testo Alt**
Testo alternativo per l’immagine.

   * **Collega a**
Il componente Immagine adattiva non utilizza questa proprietà.

   * **Descrizione**
Il componente Immagine adattiva non utilizza questa proprietà.

#### Estensione del componente Immagine adattiva {#extending-the-adaptive-image-component}

Per informazioni sulla personalizzazione del componente Immagine adattiva, consulta [Informazioni sul componente Immagine adattiva](/help/sites-developing/responsive.md#using-adaptive-images).

### Carosello {#carousel}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core carosello](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=it) invece.

Il componente Carosello consente di visualizzare le immagini associate a singole pagine:

* una per volta
* per un breve periodo
* in un ordine specificato
* con un ritardo specificato

I controlli selezionabili consentono inoltre all’utente di scorrere le pagine visualizzate in tempo reale e su richiesta. Quando si seleziona l’immagine di pagina attualmente visibile, si passa alla pagina corrispondente. In altre parole, il carosello funge da controllo di navigazione.

#### Proprietà {#properties-1}

Queste proprietà sono disponibili in due schede:

* **Carosello**
Qui si specifica il funzionamento del carosello:

   * Velocità di riproduzione Tempo in millisecondi prima della visualizzazione della diapositiva successiva.
   * Tempo di transizione Tempo in millisecondi per la transizione tra due diapositive.
   * Stile comandi Varie opzioni sono disponibili in un menu a discesa; ad esempio, Pulsanti Prec/Succ, Opzioni alto-destra.

* **Elenco**

   Qui si specifica come vengono incluse le pagine nel carosello:

   * **Genera elenco utilizzando**
Esistono diversi modi per creare un elenco di pagine: Pagine figlie, Elenco fisso, Ricerca o Ricerca avanzata (descritti di seguito).
Indipendentemente dal metodo scelto, alle pagine incluse nell’elenco deve essere già associata un’immagine alla pagina. È questa immagine che viene visualizzata nel carosello. Se non è presente un’immagine per una determinata pagina nelle Proprietà pagina di tale pagina, è necessario associare un’immagine alla pagina prima di iniziare. In caso contrario, il carosello visualizza una pagina principalmente vuota. Vedi [Modifica delle proprietà di una pagina](/help/sites-authoring/editing-page-properties.md).
A seconda dell’elemento scelto, viene visualizzato un nuovo pannello:

      * **Opzioni per le pagine secondarie**

         * **Pagina padre**
Specifica un percorso manualmente o utilizzando il selettore. Lascia vuoto per utilizzare la pagina corrente come pagina padre.
      * **Opzioni per elenco fisso**

         * **Pagine**
Seleziona un elenco di pagine. Utilizzare 
`+` per aggiungere altre voci e i pulsanti su/giù per regolare l&#39;ordine.
      * **Opzioni per la ricerca**

         * **Inizia**
Immettere un percorso iniziale, manualmente o utilizzando il selettore.

         * **Query di ricerca**
È possibile immettere una query di ricerca con testo normale.
      * **Opzioni di ricerca avanzata**

         * **Notazione predicato Querybuilder**
È possibile inserire una query di ricerca utilizzando la notazione predicato Querybuilder. Ad esempio, puoi inserire &quot;fulltext=Marketing&quot; per visualizzare nel carosello tutte le pagine con &quot;Marketing&quot; nel contenuto.
Vedi [API di QueryBuilder](/help/sites-developing/querybuilder-api.md) per una discussione completa delle espressioni di query e ulteriori esempi.
   * **Ordina per**
Seleziona 
`jcr:title`, `jcr:created`, `cq:lastModified`oppure `cq:template` dal menu a discesa .

   * **Limite**
Facoltativo. Il numero massimo di elementi che si desidera utilizzare nel carosello.





>[!NOTE]
>
>Puoi creare un componente carosello personalizzato per Adobe Experience Manager per la visualizzazione di risorse digitali nel DAM AEM. Vedi [Creazione di componenti Carosello personalizzati per Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en).

### Grafico {#chart}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Il componente Grafico consente di aggiungere un grafico a barre, a linee o a torta. AEM un grafico a partire dai dati forniti. Puoi fornire i dati digitando direttamente nella scheda Dati oppure copiando e incollando un foglio di calcolo.

* **Dati**

   * **Dati grafico**
Immetti i dati del grafico in formato CSV; il formato Valori separati da virgola utilizza virgole (&quot;,&quot;) come separatore di campo.

* **Avanzate**

   * **Tipo di grafico**
Selezionare tra Grafico a torta, Grafico a linee e Grafico a barre.

   * **Testo alternativo**
Visualizza testo alternativo invece del grafico.

   * **Larghezza**
Larghezza del grafico in pixel.

   * **Altezza**
Altezza del grafico in pixel.

Di seguito è riportato un esempio di dati del grafico seguito dal grafico a barre risultante:

![chlimage_1-89](assets/chlimage_1-89.png) ![dc_graph_use](assets/dc_chart_use.png)

>[!NOTE]
>
>Puoi creare un controllo grafico AEM personalizzato che visualizza i dati nel JCR AEM. Per informazioni, consulta [Visualizzazione dei dati di Adobe Experience Manager in un grafico](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en).

### Frammenti di contenuto {#content-fragment}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) invece.

[Frammenti di contenuto](/help/sites-authoring/content-fragments.md) vengono creati e gestiti come risorse indipendenti dalla pagina. Puoi quindi utilizzare questi frammenti, con le relative varianti, durante l’authoring di pagine di contenuto.

### Importazione progettazione {#design-importer}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Questo componente consente di caricare un file zip contenente un pacchetto di progettazione.

### Scarica {#download}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Il componente Scarica crea un collegamento nella pagina web selezionata per scaricare un file specifico. Puoi trascinare una risorsa da Content Finder oppure caricare un file.

* **Download**

   * **Descrizione**
Breve descrizione visualizzata con il collegamento di download.

   * **File**
Il file disponibile per il download nella pagina Web risultante. Trascina una risorsa da Content Finder oppure seleziona l’area per caricare il file che desideri scaricare.

L’esempio seguente mostra il componente Scarica in Geometrixx:

![dc_download_use](assets/dc_download_use.png)

### Esterno {#external}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Il componente per l’integrazione con applicazioni esterne (**Esterno**) consente di incorporare applicazioni esterne nella pagina AEM utilizzando un iframe.

* **Esterno**

   * **Applicazione di destinazione**
Specificare l&#39;URL dell&#39;applicazione web da integrare; ad esempio:

      ```
      https://en.wikipedia.org/wiki/Main_Page
      ```

   * **Passa parametri**
Se necessario, seleziona la casella per i parametri da passare all’applicazione.

   * **Larghezza e altezza **Definire le dimensioni dell’iframe

l&#39;applicazione esterna è integrata nel sistema paragrafo della pagina AEM; ad esempio, quando si utilizza un&#39;applicazione Target di `https://en.wikipedia.org/wiki/Main_Page`:

![chlimage_1-90](assets/chlimage_1-90.png)

>[!NOTE]
>
>A seconda del caso d’uso, sono disponibili altre opzioni per l’integrazione di applicazioni esterne, ad esempio la variabile [Integrazione di portlet](/help/sites-administering/aem-as-portal.md).

### Flash {#flash}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

>[!CAUTION]
>
>Non è più previsto che questo componente funzioni come standard senza un’ampia personalizzazione a livello di progetto.

Il componente Flash consente di caricare un filmato Flash. Puoi trascinare una risorsa Flash da Content Finder sul componente oppure utilizzare la finestra di dialogo:

* **Flash**

   * **Filmato Flash**

      File del filmato Flash. Potete trascinare una risorsa da Content Finder oppure fare clic per aprire una finestra con cui individuare il contenuto.

   * **Dimensione**

      Dimension in pixel dell’area di visualizzazione destinata al filmato.

* **Immagine alternativa**

   Immagine alternativa da visualizzare

* **Avanzate**

   * **Menu di scelta rapida**

      Indica se il menu di scelta rapida deve essere visualizzato o nascosto.

   * **Modalità finestra**

      Aspetto della finestra, ad esempio opaca, trasparente o distinta (solida).

   * **Colore sfondo**

      Colore di sfondo selezionato dalla tavola colori fornita.

   * **Versione minima**

      Versione minima del Flash Player di Adobe necessario per eseguire il filmato. Il valore predefinito è 9.0.0.

   * **Attributi**

      Eventuali altri attributi richiesti.

### Immagine {#image}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core immagine](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=it) invece.

Il componente Immagine visualizza un’immagine e il relativo testo in base ai parametri specificati.

Puoi caricare un’immagine, quindi modificarla e manipolarla (ad esempio, ritagliarla, ruotarla, aggiungere un collegamento/titolo/testo).

Puoi trascinare un’immagine da [Browser Risorse](/help/sites-authoring/author-environment-tools.md#assets-browser) direttamente sul componente o sul relativo [Finestra di dialogo Configura](/help/sites-authoring/editing-content.md#component-edit-dialog). Puoi anche caricare un’immagine dalla finestra di dialogo Configura (Configure); questa finestra di dialogo controlla anche tutte le definizioni e le manipolazioni dell&#39;immagine:

![chlimage_1-91](assets/chlimage_1-91.png)

Dopo il caricamento dell’immagine (e non prima), puoi utilizzare [modifica diretta](/help/sites-authoring/editing-content.md#edit-content) per ritagliare/ruotare l’immagine come necessario:

![](do-not-localize/chlimage_1-15.png)

>[!NOTE]
>
>L’editor locale utilizza le dimensioni e le proporzioni originali dell’immagine durante la modifica. È inoltre possibile specificare le proprietà relative a altezza e larghezza. Eventuali restrizioni relative a dimensioni e proporzioni definite nelle proprietà vengono applicate al salvataggio delle modifiche.
>
>A seconda dell’istanza, le restrizioni minime e massime possono essere imposte anche dal [progettazione della pagina](/help/sites-developing/designer.md). Queste restrizioni vengono sviluppate durante l&#39;implementazione del progetto.

Sono disponibili diverse opzioni aggiuntive nella modalità di modifica a schermo intero; ad esempio, mappa e zoom:

![](do-not-localize/chlimage_1-16.png)

>[!NOTE]
>
>Impossibile monitorare l&#39;avanzamento del caricamento con Internet Explorer.
>
>Gli utenti di Internet Explorer devono caricare l’immagine e fare clic su **Ok**, quindi riapri l’immagine per visualizzare il file caricato nell’anteprima e per poter eseguire modifiche (ovvero, ritagliare).
>
>Consulta la sezione [Piattaforme certificate](/help/release-notes/release-notes.md#certifiedplatforms) per ulteriori informazioni sulle funzioni di HTML5 utilizzate da AEM.

Quando un’immagine viene caricata, puoi configurare quanto segue:

* **Mappa**

   Per mappare un’immagine, seleziona Mappa. È possibile specificare come si desidera creare la mappa immagine (rettangolare, poligonale e così via) e la destinazione dell’area.

* **Ritaglia**

   Per estrarre parte di un&#39;immagine, selezionare Ritaglia. Utilizza il mouse per ritagliare l&#39;immagine.

* **Rotazione**

   Per ruotare un’immagine, selezionate Ruota. Utilizzare ripetutamente finché l&#39;immagine non viene ruotata nel modo desiderato.

* **Cancella**

   Rimuovi l&#39;immagine corrente.

* **Titolo**

   Titolo dell’immagine.

* **Testo Alt**

   Testo alternativo da utilizzare per la creazione di contenuto accessibile.

* **Collega a**

   Crea un collegamento a risorse o altre pagine all’interno del sito web.

* **Descrizione**

   Una descrizione dell’immagine.

* **Dimensione**

   Imposta l’altezza e la larghezza dell’immagine.

>[!NOTE]
>
>Alcune opzioni sono disponibili solo nell’editor a schermo intero.

L&#39;immagine finale (con **Titolo** e **Descrizione**) può essere visualizzata come:

![chlimage_1-92](assets/chlimage_1-92.png)

### Contenitore di layout {#layout-container}

Questo componente fornisce un sistema paragrafo a griglia che consente di aggiungere e posizionare i componenti all’interno di un [griglia reattiva](/help/sites-authoring/responsive-layout.md). Puoi definire layout di contenuti diversi in base alla larghezza dei dispositivi di destinazione, compresi una serie di telefoni, tablet e desktop.

![chlimage_1-93](assets/chlimage_1-93.png)

>[!NOTE]
>
>Questo componente è stato implementato con [Linguaggio dei modelli di HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it).

### Elenco {#list}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Elenco componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html) invece.

Il componente Elenco consente di configurare i criteri di ricerca per la visualizzazione di un elenco:

* **Elenco**

   * **Genera elenco con**

      Qui si specifica dove l’elenco recupera il relativo contenuto. Esistono diversi metodi:

   * A seconda dell’elemento scelto, viene visualizzato un nuovo pannello:

      * **Opzioni per le pagine secondarie**

         * **Bambini di** (Pagina padre)

            Specifica un percorso manualmente o utilizzando il selettore. Lascia vuoto per utilizzare la pagina corrente come pagina padre.
      * **Opzioni per elenco fisso**

         * **Pagine**

            Seleziona un elenco di pagine. Utilizza + per aggiungere altre voci e i pulsanti su/giù per regolare l’ordine.
      * **Opzioni per la ricerca**

         * Inizia in

            Immettere un percorso iniziale, manualmente o utilizzando il selettore.

         * Query di ricerca

            È possibile immettere una query di ricerca con testo normale.
      * **Opzioni di ricerca avanzata**

         * **Notazione predicato Querybuilder**

            È possibile inserire una query di ricerca utilizzando la notazione predicato Querybuilder. Ad esempio, puoi inserire &quot;fulltext=Marketing&quot; per visualizzare nel carosello tutte le pagine con &quot;Marketing&quot; nel contenuto.

            Vedi [API di QueryBuilder](/help/sites-developing/querybuilder-api.md) per una discussione completa delle espressioni di query e ulteriori esempi.
      * **Tag**

         Specifica la **Pagina padre**, **Tag/Parole chiave** e i criteri di corrispondenza richiesti.
   * **Visualizza come**

      Come si desidera che gli elementi siano elencati; include collegamenti, teaser e notizie.

   * **Ordina per**

      Se l’elenco deve essere ordinato e, in tal caso, i criteri da utilizzare per l’ordinamento. Puoi immettere un criterio o selezionarne uno dall’elenco a discesa fornito.

   * **Limite**

      Specifica il numero massimo di elementi da visualizzare nell’elenco.

   * **Abilita feed**

      Indica se attivare un feed RSS per l’elenco.

   * **Paginare dopo**

      Qui è possibile specificare il numero di voci da visualizzare contemporaneamente. Un elenco con più elementi di quanto specificato utilizza l’impaginazione per visualizzare l’elenco in più parti.






L’esempio seguente mostra un **Elenco** per la visualizzazione di un elenco di pagine figlie (la progettazione è controllata dalle definizioni CSS personalizzate di una progettazione del sito).

![dc_list_use](assets/dc_list_use.png)

### Accesso {#login}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

>[!CAUTION]
>
>Non è più previsto che questo componente funzioni come standard senza un’ampia personalizzazione a livello di progetto.

Fornisce i campi Nome utente e Password .

![chlimage_1-94](assets/chlimage_1-94.png)

Puoi configurare i seguenti parametri:

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

### Stato ordine {#order-status}

>[!CAUTION]
>
>Non è più previsto che questo componente funzioni come standard senza un’ampia personalizzazione a livello di progetto.

* **Titolo**

   * **Titolo**

      Specificare il testo del titolo che si desidera visualizzare.

   * **Collegamento**

      Specifica la pagina (prodotto) per la quale deve essere visualizzato lo stato dell’ordine.

   * **Tipo/Dimensione**

      Seleziona dalla selezione fornita.

![chlimage_1-95](assets/chlimage_1-95.png)

### Riferimento {#reference}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) invece.

La **Riferimento** consente di fare riferimento a testo da un’altra pagina del sito web AEM (nell’istanza corrente). Il contenuto del paragrafo a cui si fa riferimento viene visualizzato come se si trovasse nella pagina corrente. Il contenuto viene aggiornato quando il paragrafo sorgente cambia (potrebbe essere necessario un aggiornamento della pagina).

* **Riferimento paragrafo**

   * **Riferimento**

      Specifica il percorso della pagina e il paragrafo a cui fare riferimento (includere il contenuto).

Per specificare il percorso di un paragrafo, è necessario aggiungere come suffisso il percorso (della pagina) con:

`.../jcr:content/par/<paragraph-ID>`

Esempio:

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par/similar-products`

Oltre a fare riferimento a un paragrafo specifico, il percorso può anche essere modificato per specificare un sistema di paragrafi completo. Per eseguire questa operazione, è necessario aggiungere al percorso un suffisso con il seguente:

`/jcr:content/par`

Esempio:

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par`

Dopo la configurazione, il contenuto viene visualizzato esattamente come nella pagina sorgente. Il fatto che si tratti di un riferimento viene visualizzato solo quando si apre il componente per la modifica:

![chlimage_1-96](assets/chlimage_1-96.png)

### Ricerca {#searching}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core di ricerca rapida](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/quick-search.html) invece.

Il componente Ricerca aggiunge funzionalità di ricerca alla pagina.

Puoi configurare i seguenti parametri:

* Ricerca

   * **Tipi di nodo**

      Se la ricerca deve essere limitata a specifici tipi di nodo elencali qui; ad esempio, `cq:Page`.

   * **Percorso di ricerca**

      Specificare la pagina principale del ramo che si desidera cercare.

   * **Testo pulsante Cerca**

      Nome visualizzato sul pulsante di ricerca effettivo.

   * **Testo per le statistiche**

      Testo visualizzato sopra i risultati della ricerca.

   * **Testo Nessun risultato**

      In assenza di risultati, viene visualizzato il testo inserito qui.

   * **Controllo ortografia del testo**

      Se un utente immette un termine simile, questo testo viene visualizzato prima del termine.
Ad esempio, se digiti `Geometrixxe`, il sistema mostra &quot;Intendevi? Geometrixx&quot;.

   * **Testo per pagine simili**

      Testo visualizzato accanto a un risultato per pagine simili. Per visualizzare pagine con contenuti simili, fai clic su questo collegamento.

   * **Testo di ricerche correlate**

      Testo visualizzato accanto a ricerche per termini e argomenti correlati.

   * **Testo delle tendenze di ricerca**

      Titolo al di sopra dei termini di ricerca immessi da un utente.

   * **Etichetta pagina risultati**

      Testo visualizzato in fondo all’elenco con collegamenti alle altre pagine dei risultati.

   * **Etichetta precedente**

      Nome visualizzato sul collegamento alle pagine di ricerca precedenti.

   * **Etichetta successiva**

      Nome visualizzato sul collegamento alle pagine di ricerca successive.

L’esempio seguente mostra il componente Ricerca dopo una ricerca per la parola *`geometrixx`* dalla directory principale di un&#39;installazione standard. Illustra inoltre la paginazione dei risultati:

![dc_search_use](assets/dc_search_use.png)

L’esempio seguente mostra un termine di ricerca errato e non disponibile:

![dc_search_usenotfound](assets/dc_search_usenotfound.png)

### Sitemap {#sitemap}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Navigazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/navigation.html), [Navigazione lingua](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/language-navigation.html)e [Componenti core Breadcrumb](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/breadcrumb.html) invece.

Un elenco automatico di mappa del sito, che (con le impostazioni predefinite) elenca tutte le pagine (come collegamenti attivi) del sito Web corrente. Ad esempio, un estratto mostra:

![dc_sitemap_use](assets/dc_sitemap_use.png)

Se necessario, puoi configurare quanto segue:

* **Sitemap**

   * **Percorso directory principale**

      Percorso da cui deve iniziare l’elenco.

### Presentazione {#slideshow}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core carosello](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=it) invece.

>[!CAUTION]
>
>Non è più previsto che questo componente funzioni come standard senza un’ampia personalizzazione a livello di progetto.

Questo componente consente di caricare una serie di immagini da visualizzare come presentazione sulla pagina. È possibile aggiungere o rimuovere immagini e assegnare a ciascuna un titolo. In Avanzate è inoltre possibile specificare la dimensione dell’area di visualizzazione.

Puoi configurare i seguenti parametri:

* **Diapositive**

   * **Nuova diapositiva**

      È possibile specificare una selezione di diapositive utilizzando **Aggiungi** e **Rimuovi**).

   * **Titolo**

      Se necessario, specifica un titolo. Il titolo viene sovrapposto alla diapositiva appropriata.

* **Avanzate**

   * **Dimensione**

      Specifica la larghezza e l’altezza in pixel.

Il componente Presentazione visualizza quindi ripetutamente ciascuna in sequenza, per un breve periodo di tempo, prima di passare alla diapositiva successiva:

![dc_slideshow_use](assets/dc_slideshow_use.png)

### Tabella {#table}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core testo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html) invece.

>[!NOTE]
>
>La **Tabella** Il componente di base è basato su [Editor Rich Text](/help/sites-authoring/rich-text-editor.md), come **[Testo](#text)** Componente di base.

La **Tabella** Il componente è preconfigurato per consentire la creazione, il riempimento e il formato di una tabella. Tramite la finestra di dialogo è possibile configurare la tabella e creare il contenuto in uno dei modi seguenti:

* da zero
* copiare e incollare un foglio di calcolo o una tabella da un editor esterno (come Excel, OpenOffice e Blocco note).

Puoi apportare modifiche di base al contenuto utilizzando l’editor in linea:

![dc_table](assets/dc_table.png)

In modalità a schermo intero è possibile configurare il layout della tabella:

![chlimage_1-97](assets/chlimage_1-97.png)

La schermata seguente mostra un esempio del componente tabella; la progettazione è determinata dal CSS specifico per il sito:

![dc_table_use](assets/dc_table_use.png)

### Tag cloud {#tag-cloud}

Una nuvola di tag mostra graficamente una selezione di tag applicati al contenuto del sito web:

![dc_tagclouduse](assets/dc_tagclouduse.png)

Durante la configurazione del componente Tag Cloud, puoi specificare:

* **Tag da visualizzare**

   Da dove vengono raccolti i tag da visualizzare. Seleziona da una pagina, da una pagina con tutte le pagine figlie o tutti i tag.

* **Pagina**

   Seleziona la pagina a cui fare riferimento.

* **Nessun collegamento sui tag**

   Indica se i tag visualizzati devono fungere da collegamenti.

Per ulteriori informazioni sull’applicazione dei tag, visita [Utilizzo dei tag](/help/sites-authoring/tags.md).

### Testo {#text}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core testo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html) invece.

>[!NOTE]
>
>La **Testo** Il componente di base è basato su [Editor Rich Text](/help/sites-authoring/rich-text-editor.md), come **Tabella** Componente di base.

Il componente Testo consente di inserire un blocco di testo utilizzando un editor WYSIWYG, con funzionalità fornite da [Editor Rich Text](/help/sites-authoring/rich-text-editor.md). Una selezione di icone consente di formattare il testo, con caratteristiche del font, allineamento, collegamenti, elenchi e rientri.

![chlimage_1-98](assets/chlimage_1-98.png)

Quando apri la **Configura** è inoltre possibile impostare:

* **Spaziatore**
* **Stile di testo**

Il testo formattato viene visualizzato sulla pagina. La progettazione effettiva dipende dal CSS del sito:

![dc_text_use](assets/dc_text_use.png)

Per informazioni più dettagliate sul componente Testo e sulla funzionalità fornita dall’editor Rich Text, consulta la sezione [Editor Rich Text](/help/sites-authoring/rich-text-editor.md) pagina.

#### Modifica locale {#inplace-editing}

Oltre alla modalità di modifica Rich Text basata su finestra di dialogo, AEM fornisce anche [Modifica locale](/help/sites-authoring/editing-content.md), che consente di modificare direttamente il testo visualizzato nel layout della pagina.

### Testo e immagine {#text-image}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Immagine](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=it) e [Componente core testo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html) invece.

Il componente Testo e immagine aggiunge un blocco di testo e un’immagine. È inoltre possibile aggiungere e modificare testo e immagini separatamente. Consulta la sezione [Testo](#text) e [Immagine](#image) componenti per dettagli.

![chlimage_1-99](assets/chlimage_1-99.png)

Puoi configurare i seguenti parametri:

* **Stili dei componenti** (**Stili**)

   Qui puoi allineare l’immagine a sinistra o a destra. Il valore predefinito è **Sinistra** allineata, con l&#39;immagine a sinistra.

* **Proprietà immagine** (**Proprietà immagine avanzate**)

   Consente di specificare quanto segue:

   * **Risorsa immagine**

      Carica l’immagine richiesta.

   * **Titolo**

      Titolo del blocco, visualizzato al passaggio del mouse.

   * **Testo Alt**

      Testo alternativo che verrà mostrato qualora l’immagine non sia disponibile. Se lasciato vuoto, viene utilizzato il titolo.

   * **Collega a**

      Specifica un percorso di destinazione.

   * **Descrizione**

      Una descrizione dell’immagine.

   * **Dimensione**

      Imposta l’altezza e la larghezza dell’immagine.

L’esempio seguente mostra un componente Testo e immagine che visualizza l’immagine allineata a sinistra:

![dc_textimage_use](assets/dc_textimage_use.png)

### Titolo {#title}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core titolo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en) invece.

Il componente Titolo può:

* Visualizza il nome della pagina corrente lasciando vuoto il campo Titolo .
* Visualizza un testo specificato nel campo Titolo.

Puoi configurare i seguenti parametri:

* **Titolo**

   Se desideri utilizzare un nome diverso dal titolo della pagina, inseriscilo qui.

* **Collegamento**

   URI se il titolo deve fungere da collegamento.

* **Tipo/Dimensione**

   Selezionare Piccolo o Grande dall’elenco a discesa. Piccolo viene generato come immagine. Grande viene generato come testo.

L’esempio seguente mostra un **Titolo** componente visualizzato; la progettazione è determinata dal CSS specifico per il sito.

![dc_title_use](assets/dc_title_use.png)

### Video {#video}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente di incorporamento componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html) invece.

>[!CAUTION]
>
>Non è più previsto che questo componente funzioni come standard senza un’ampia personalizzazione a livello di progetto.

La **Video** permette di inserire un elemento video predefinito pronto all’uso in una pagina.

Vedi anche [Configurare i profili video](/help/sites-administering/config-video.md#configuringvideoprofiles) da utilizzare con gli elementi di HTML5.

Dopo aver posizionato un’istanza del componente sulla pagina, puoi configurare quanto segue:

* Video

   * **Risorsa video**

      Carica o rilascia la risorsa video.

   * **Dimensione**

      Le dimensioni native del video (larghezza x altezza in pixel) vengono visualizzate nelle caselle accanto a Dimensioni (vedi sopra). Immetti manualmente le dimensioni di larghezza e altezza per sovrascrivere le dimensioni native del video. Selezione **OK** chiude la finestra di dialogo.

>[!NOTE]
>
>I formati supportati includono:
>
>* `.mp4`
>* `Ogg`
>* `FLV` (video Flash)


## Colonne {#columns}

Le colonne sono un meccanismo per controllare il layout del contenuto in AEM. In un’installazione standard vengono forniti componenti per la creazione di due o tre colonne.

L’esempio seguente mostra il componente Colonne in uso. È possibile utilizzare i segnaposto per i nuovi componenti:

![dc_columncontroluse](assets/dc_columncontroluse.png)

### 2 Colonne {#columns-1}

Componente Controllo colonna con impostazione predefinita di due colonne uguali.

### 3 Colonne {#columns-2}

Componente Controllo colonna con impostazione predefinita di tre colonne uguali.

### Controllo colonna {#column-control}

Il componente Controllo colonna consente agli utenti di selezionare in che modo desiderano dividere in più colonne il contenuto del pannello principale della pagina web. Gli utenti possono selezionare il numero di colonne desiderato (da un elenco predefinito) e quindi creare, eliminare o spostare il contenuto all’interno di ciascuna colonna.

* **Controllo colonna**

   * **Layout colonna**

      Selezionare il numero di colonne di cui si desidera eseguire il rendering. Una volta creata, ogni colonna dispone di un proprio collegamento per trascinare componenti o risorse durante l’aggiunta di contenuto.

## Modulo {#form}

>[!CAUTION]
>
>Il componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

I componenti modulo vengono utilizzati per creare moduli che consentono ai visitatori di inviare contributi. Forms e i componenti per moduli possono essere utilizzati per raccogliere informazioni quali feedback dagli utenti (ad esempio, un questionario sulla soddisfazione del cliente) e informazioni sugli utenti (ad esempio, registrazione utente).

>[!NOTE]
>
>Vedi [Guida di AEM Forms](/help/forms/home.md) per informazioni su AEM Forms.

Forms è costituito da diversi componenti diversi:

* **Modulo**

   Il componente Modulo definisce l’inizio e la fine di un nuovo modulo sulla pagina. È quindi possibile inserire altri componenti tra questi elementi, ad esempio tabelle e download.

* **Campi ed elementi modulo**

   I campi e gli elementi modulo possono includere caselle di testo, pulsanti di scelta e immagini. L’utente spesso completa un’azione in un campo modulo, ad esempio digita del testo. Per ulteriori informazioni, consulta la sezione sui singoli elementi del modulo .

* **Componenti del profilo**

   I componenti profilo si riferiscono ai profili dei visitatori utilizzati per collaborazione social e altre aree in cui è richiesta la personalizzazione in base al visitatore.

Di seguito è riportato un esempio di modulo. È composto dal **Modulo** componente (inizio e fine), con due **Modulo** **Testo** campi utilizzati per l’input, a **Generale** **Testo** campo utilizzato per il testo introduttivo e un **Invia** pulsante .

![dc_form](assets/dc_form.png)

>[!NOTE]
>
>Le informazioni sullo sviluppo e la personalizzazione dei moduli sono disponibili nella sezione [Pagina Sviluppo di Forms](/help/sites-developing/developing-forms.md). Questa funzionalità include l’aggiunta di azioni, vincoli, precaricamento di campi e l’utilizzo di script per richiamare un servizio all’azione, tra gli altri.

### Impostazioni comuni a (molti) componenti modulo {#settings-common-to-many-form-components}

Sebbene ciascuno dei componenti modulo abbia uno scopo diverso, molti sono composti da opzioni e parametri simili.

Quando si configura un componente modulo, nella finestra di dialogo sono disponibili le seguenti schede:

* **Titolo e testo**

   Qui si specificano le informazioni di base, ad esempio il titolo del modulo ed eventuale testo di corredo. Se appropriato è inoltre possibile definire altre informazioni chiave, ad esempio se il campo è selezionabile in più elementi e quali possono essere selezionati.

* **Valori iniziali**

   Consente di specificare un valore predefinito.

* **Vincoli**

   Qui è possibile specificare se un campo è obbligatorio ed eventuali vincoli associati al campo (ad esempio se il valore deve essere numerico).

* **Attribuzione stile**

   Indica la dimensione e lo stile dei campi.

>[!NOTE]
>
>I campi disponibili variano notevolmente a seconda del singolo componente.

Queste schede forniscono i parametri necessari. Le schede possono dipendere dal singolo tipo di componente, ma possono includere quanto segue:

* **Titolo e testo**

   * **Nome elemento**

      Nome dell’elemento modulo. Indica dove nel repository i dati vengono memorizzati.
Questo campo è obbligatorio e deve contenere solo i seguenti caratteri:

      * caratteri alfanumerici
      * `_ . / : -`
   * **Titolo**

      Titolo visualizzato con il campo . Se lasciato vuoto, viene visualizzato il titolo predefinito.

   * **Descrizione**

      Consente di fornire informazioni aggiuntive per l’utente, se necessario. Sul modulo, viene visualizzato sotto il campo, in un font più piccolo rispetto al titolo.

   * **Mostra/Nascondi**

      Determina quando il campo è visibile.


* **Valori iniziali**

   * **Valore predefinito**

      Il valore visualizzato nel campo all’apertura del modulo. Cioè, prima che l&#39;utente abbia effettuato qualsiasi input.

* **Vincoli**

   * **Obbligatorio**

      I vincoli dipendono dal tipo di componente modulo, ma fornisce una o più caselle di controllo per indicare che il campo è obbligatorio o che alcune parti di esso sono obbligatorie.

   * **Messaggio richiesto**

      Messaggio per informare gli utenti che questo campo è obbligatorio. Anche un campo obbligatorio è contrassegnato da un asterisco.

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

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core contenitore modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html) invece.

Il componente Modulo definisce l’inizio e la fine di un modulo mediante l’uso della **Inizio modulo** e **Fine modulo** elementi. L’inizio e la fine sono sempre associati per garantire che il modulo sia definito correttamente.

![dc_form-1](assets/dc_form-1.png)

Tra l’inizio e la fine di un modulo è possibile aggiungere componenti modulo che definiscono i campi di immissione effettivi per gli utenti.

>[!NOTE]
>
>Il componente modulo dei componenti di base supporta solo l’utilizzo di altri componenti modulo dei componenti di base (pulsante, testo, nascosto e così via). Utilizzo [componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) i componenti modulo all’interno di un modulo componente di base (e viceversa) non sono supportati.

#### Inizio del modulo {#start-of-form}

Questo componente definisce l’inizio di un nuovo modulo su una pagina. Puoi configurare i seguenti parametri:

* **Modulo**

   * **Pagina di ringraziamento**

      Pagina a cui fare riferimento per ringraziare i visitatori dopo aver fornito il proprio input. Se viene lasciato vuoto, dopo l’invio viene nuovamente visualizzato il modulo.

   * **Avvia flusso di lavoro**

      Determina il flusso di lavoro che viene attivato dopo l’invio del modulo.

* **Avanzate**

   * **Tipo di azione**

      Un modulo richiede un’azione. L’azione definisce l’operazione che viene attivata per l’esecuzione con i dati inviati dall’utente (simile a action= in HTML). Alcuni hanno bisogno di **Configurazione azione**.
Una selezione di tipi di azioni è inclusa in un’installazione standard AEM:

      * **Richiesta account**
      * **Crea contenuto**
      * **Crea lead**
      * **Crea e aggiorna account**
      * **Servizio e-mail: crea utente con sottoscrizione e aggiungi all&#39;elenco**
      * **Servizio e-mail: invia messaggio di risposta automatica**
      * **Servizio e-mail: annulla sottoscrizione a mailing list**
      * **Modifica community**
      * **Modifica risorse**
      * **Modifica risorse controllate da flusso di lavoro**
      * **Mail**
      * **Dettagli ordine inoltrato**
      * **Aggiornamento profilo**
      * **Ripristina password**
      * **Imposta password**
      * **Contenuto store**

         Il tipo di azione predefinito.

      * **Contenuto store con caricamenti**
      * **Invia ordine**
      * **Annulla sottoscrizione utente**
      * **Aggiorna ordine**
   * **Identificatore modulo**

      L’identificatore del modulo identifica il modulo in modo univoco. Utilizzare l’identificatore del modulo se sono presenti più moduli su una singola pagina; assicurati che abbiano identificatori diversi.

   * **Percorso di caricamento**

      Percorso delle proprietà nodo utilizzato per caricare valori predefiniti nei campi del modulo.

      Un campo facoltativo che specifica il percorso di un nodo nel repository. Quando le proprietà di questo nodo corrispondono ai nomi dei campi, i campi appropriati del modulo vengono precaricati con il valore di tali proprietà. Se non esiste alcuna corrispondenza, il campo contiene il valore predefinito.

      Utilizzo **Percorso di caricamento** è possibile precaricare il modulo con i valori inseriti nei campi richiesti. Vedi [Precaricamento dei valori dei moduli](/help/sites-developing/developing-forms.md#preloading-form-values).

   * **Convalida client**

      Indica se il modulo richiede la convalida client (convalida server) *sempre* si verifica). È possibile eseguire la convalida client con **Forms Captcha** componente.

   * **Tipo risorsa validazione**

      Definisce il tipo di risorsa per la convalida del modulo se si desidera convalidare l’intero modulo (anziché i singoli campi). Se si convalida l’intero modulo, includere anche uno dei seguenti elementi:

      * Uno script per la convalida client:

         `/apps/<*myApp*>/form/<*myValidation*>/formclientvalidation.jsp`

      * Uno script per la convalida sul lato server:

         `/apps/<*myApp*>/form/<*myValidation*>/formservervalidation.jsp`
   * **Configurazione azione**

      Le opzioni disponibili in **Configurazione azione** dipende dal **Tipo di azione**:

      * **Richiesta account**

         * **Pagina di creazione account**

            Pagina utilizzata per creare un account.
      * **Crea contenuto**

         * Percorso contenuto

            Percorso di contenuto per qualsiasi contenuto riprodotto nel modulo. Immettere un percorso che termina con una barra `/`. La barra indica che per ogni porta del modulo viene creato un nuovo nodo nel percorso specificato; ad esempio:

            `/forms/feedback/`

         * **Tipo**

            Seleziona il tipo richiesto.

         * **Modulo**

            Specificare il modulo.

         * **Rendering con**

            Seleziona l’opzione desiderata dall’elenco.

         * **Tipo risorsa**

            Se impostato, viene aggiunto a ogni commento come `sling:resourceType`

         * **Selettore vista**
      * **Crea lead**

         * **Il lead viene aggiunto a questo elenco**

            Specifica l’elenco di lead richiesto.
      * **Crea e aggiorna account**

         * **Gruppo iniziale**

            Gruppo a cui assegnare il nuovo utente.

         * **Pagina principale**

            Pagina da visualizzare dopo l’accesso.

         * **Percorso**

            Percorso (relativo) per la creazione e la memorizzazione del nuovo account.

         * **Visualizza dati...**

            Selezionando questo pulsante è possibile accedere alle informazioni sui risultati del modulo nell’Editor in serie. Da qui puoi esportare le informazioni in un `.tsv` File (separato da tabulazioni) da utilizzare, ad esempio, in un foglio di calcolo Excel.
      * **Mail**

         * **Da**

            Immetti l’indirizzo e-mail dal quale deve essere inviato il messaggio e-mail.

         * **Invia a**

            Immettere uno o più indirizzi e-mail a cui viene inviato il modulo.

         * **CC**

            Inserisci uno o più indirizzi e-mail CC.

         * **CCN**

            Inserisci uno o più indirizzi e-mail CCN.

         * **Oggetto**

            Immetti l’oggetto dell’e-mail.
      * **Ripristina password**

         * **Pagina modifica password**

            Pagina utilizzata per modificare la password.
      * **Contenuto store**

         * **Percorso contenuto**

            Percorso di contenuto per qualsiasi contenuto riprodotto nel modulo. Immettere un percorso che termina con una barra `/`. La barra indica che per ogni porta del modulo viene creato un nuovo nodo nel percorso specificato; ad esempio:
            `/forms/feedback/`

         * **Visualizza dati...**

            Fare clic su questo pulsante per accedere alle informazioni sui risultati del modulo nell’Editor in serie. Da qui puoi esportare le informazioni in un file .tsv (separato da tabulazioni) da utilizzare, ad esempio, in un foglio di calcolo Excel.
      * **Contenuto store con caricamenti**

         Ha le stesse opzioni di **Contenuto store**.

      * **Annulla sottoscrizione utente**

         * **Il lead viene eliminato da questo elenco**

            Specifica l’elenco di lead richiesto.










#### Fine del modulo {#end-of-form}

Contrassegna la fine del modulo. Puoi configurare quanto segue:

* **Fine modulo**

   * **Mostra pulsante Invia**

      Indica se mostrare o meno un pulsante Invia.

   * **Nome invio**

      Identificatore, se si utilizzano più pulsanti Invia in un modulo.

   * **Titolo invio**

      Nome visualizzato sul pulsante, ad esempio Invia.

   * **Mostra pulsante Ripristina**

      Quando si seleziona la casella di controllo, il pulsante Ripristina diventa visibile.

   * **Titolo ripristino**

      Nome visualizzato sul pulsante Ripristina.

   * **Descrizione**

      Informazioni visualizzate sotto il pulsante.

### Nome account {#account-name}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente di base Testo modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html) invece.

Consente all’utente di inserire un nome account:

![dc_form_account_name](assets/dc_form_accountname.png)

### Indirizzo {#address}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente di base Testo modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html) invece.

Consente di aggiungere un campo di indirizzo internazionale nel seguente formato:

![dc_form_addressfield](assets/dc_form_addressfield.png)

Il componente è configurato per l’uso immediato, ma se necessario puoi modificare la configurazione. Ad esempio, è possibile aggiungere vincoli per i singoli elementi dell’indirizzo . Se i campi rimangono vuoti, vengono utilizzate le impostazioni predefinite.

### Captcha {#captcha}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

>[!CAUTION]
>
>Non è più previsto che questo componente funzioni come standard senza un’ampia personalizzazione a livello di progetto.

Il componente Captcha richiede all’utente di digitare una stringa alfanumerica come visualizzata sullo schermo. La stringa cambia con ogni aggiornamento.

![dc_form_captcha](assets/dc_form_captcha.png)

Puoi configurare vari parametri per questo componente, incluso un messaggio da visualizzare quando la stringa captcha non è valida.

### Gruppo di caselle di selezione {#checkbox-group}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core Opzioni modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html) invece.

Una casella di controllo consente di creare un elenco di una o più caselle di controllo, molte delle quali possono essere selezionate contemporaneamente.

![dc_form_checkboxgroupuse](assets/dc_form_checkboxgroupuse.png)

Puoi specificare vari parametri, tra cui un titolo, una descrizione e un nome di elemento. Utilizzando i pulsanti + e - è possibile aggiungere o rimuovere elementi, quindi posizionarli con le frecce su e giù.

>[!NOTE]
>
>Utilizzo **Percorso di caricamento elementi** è possibile precaricare l’elenco dei gruppi di caselle di controllo con i relativi valori.
>
>Vedi [Precaricamento dei campi modulo con più valori](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Dati carta di credito {#credit-card-details}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Consente di specificare i campi necessari per l&#39;immissione dei dettagli della carta di credito. Puoi configurarlo per specificare i tipi di scheda accettati e le informazioni richieste (ad esempio, il codice di sicurezza).

![chlimage_1-100](assets/chlimage_1-100.png)

### Elenco a discesa {#dropdown-list}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core Opzioni modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html) invece.

Un elenco a discesa può essere configurato per fornire all’utente una serie di valori da selezionare:

![dc_form_dropdownlistuse](assets/dc_form_dropdownlistuse.png)

È possibile specificare un titolo e gli elementi da visualizzare nell’elenco. Utilizzando i pulsanti + e - è possibile aggiungere o rimuovere le voci dell’elenco, quindi posizionarle con i pulsanti Su e Giù . È possibile specificare se gli utenti possono selezionare più elementi dall’elenco e tutti gli elementi che devono essere selezionati automaticamente la prima volta che aprono l’elenco (valori iniziali).

>[!NOTE]
>
>Utilizzo **Percorso di caricamento elementi** puoi precaricare l’elenco a discesa con i relativi valori.
>
>Vedi [Precaricamento dei campi modulo con più valori](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Caricamento di file {#file-upload}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Il componente Caricamento file offre all’utente la possibilità di selezionare e caricare un file.

![dc_form_fileupload](assets/dc_form_fileupload.png)

>[!NOTE]
>
>Puoi creare un componente di caricamento personalizzato per caricare i file su un servlet Sling. Per informazioni, consulta [Caricamento di file in Adobe Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-cloud-service-create-asset-servlet-for-uploading-small-files/td-p/404276).

### Campo nascosto {#hidden-field}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente di base nascosto per modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-hidden.html) invece.

Consente di creare un campo nascosto. Questi campi nascosti possono essere utilizzati per vari scopi. Ad esempio, quando è necessario eseguire un’azione dopo l’invio del modulo o quando i dati nascosti sono necessari in fase di post-elaborazione.

![dc_form_hiddenfield](assets/dc_form_hiddenfield.png)

>[!NOTE]
>
>È inoltre possibile personalizzare il modulo in modo da mostrare o nascondere specifici componenti in base al valore di altri campi del modulo. La modifica della visibilità di un campo modulo è utile quando il campo è necessario solo in presenza di condizioni specifiche.
>
>Vedi [Mostrare e nascondere i componenti di un modulo](/help/sites-developing/developing-forms.md#showing-and-hiding-form-components).

### Pulsante immagine {#image-button}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core pulsante modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html) invece.

Un pulsante immagine consente di creare un pulsante con immagine e testo personalizzati:

![dc_form_imagebutton](assets/dc_form_imagebutton.png)

### Caricamento immagine {#image-upload}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Il componente Caricamento immagine offre all’utente la possibilità di selezionare e caricare un file di immagine.

![dc_form_imageupload](assets/dc_form_imageupload.png)

### Campo collegamento {#link-field}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Il campo di collegamento consente all’utente di specificare un URL:

![dc_form_link](assets/dc_form_link.png)

Viene utilizzato frequentemente per il modulo evento calendario, in cui è utilizzato per il campo URL/collegamento di un evento.

### Campo password {#password-field}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Consente all’utente di inserire la propria password:

![dc_form_password](assets/dc_form_password.png)

### Reimpostazione password {#password-reset}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Questo componente fornisce all’utente due campi:

* immissione di una password
* inserimento ripetuto della password per verificare che l&#39;input sia corretto.

Con le impostazioni predefinite, il componente viene visualizzato come segue:

![dc_password_reset](assets/dc_password_reset.png)

### Gruppo pulsanti di scelta {#radio-group}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core Opzioni modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html) invece.

Un gruppo pulsanti di scelta fornisce un elenco di una o più caselle di controllo, una sola delle quali può essere selezionata in un determinato momento.

Puoi specificare il nome dell’elemento insieme a un titolo e a una descrizione. Utilizzando i pulsanti + e - è possibile aggiungere o rimuovere elementi, posizionarli con le frecce su e giù e specificare un valore predefinito, se necessario:

![dc_form_radiogroupuse](assets/dc_form_radiogroupuse.png)

>[!NOTE]
>
>Utilizzo **Percorso di caricamento elementi** puoi precaricare il gruppo pulsanti di scelta con i relativi valori.
>
>Vedi [Precaricamento dei campi modulo con più valori](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Pulsante Invia {#submit-button}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core pulsante modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html) invece.

Questo componente consente di creare un pulsante di invio, con il testo predefinito:

![dc_form_submitbutton](assets/dc_form_submitbutton.png)

Oppure con il tuo testo:

![dc_form_submitbuttonuse](assets/dc_form_submitbuttonuse.png)

### Campo tag {#tags-field}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) invece.

Questo campo consente di selezionare i tag:

![dc_form_tags_use](assets/dc_form_tags_use.png)

Puoi specificare vari parametri, inclusi i namespace utilizzabili, utilizzando la scheda apposita:

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

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente di base Testo modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html) invece.

Il campo di testo standard può essere configurato in base alle dimensioni richieste e con un messaggio lead in:

![dc_form_text](assets/dc_form_text.png)

### Pulsanti invio flusso di lavoro {#workflow-submit-button-s}

>[!CAUTION]
>
>Questo componente di base è obsoleto. L&#39;Adobe consiglia di utilizzare [Componente core pulsante modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html) invece.

Consente di creare un pulsante Invia da utilizzare in un flusso di lavoro.

![chlimage_1-101](assets/chlimage_1-101.png)
