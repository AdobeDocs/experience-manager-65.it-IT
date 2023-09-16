---
title: Amministrazione di eCommerce generico
description: La soluzione generica dell’AEM fornisce metodi per gestire le informazioni commerciali contenute nell’archivio.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: b00ed4ed146b89aece9af1d267c890a360a236e9
workflow-type: tm+mt
source-wordcount: '2929'
ht-degree: 2%

---

# Amministrazione di eCommerce generico {#administering-generic-ecommerce}

La soluzione generica Adobe Experience Manager (AEM) fornisce metodi per gestire le informazioni di e-commerce conservate all’interno dell’archivio (anziché utilizzare un motore di e-commerce esterno). Ciò include:

* [Prodotti](/help/commerce/cif-classic/administering/concepts.md#products)
* [Varianti prodotto](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [Cataloghi](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [Promozioni](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [Voucher](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [Ordini](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Pagine proxy](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>L’installazione standard dell’AEM include l’implementazione eCommerce generica dell’AEM (JCR).
>
>Questo è a scopo dimostrativo o come base per un’implementazione personalizzata in base alle tue esigenze.

## Prodotti e varianti di prodotto {#products-and-product-variations}

>[!NOTE]
>
>Le procedure seguenti si applicano sia ai prodotti che alle varianti di prodotto.

Prima di creare i prodotti, definisci un [impalcatura](/help/sites-authoring/scaffolding.md). Specifica i campi da definire, i prodotti e la modalità di modifica.

È necessario uno scaffold per ogni tipo di prodotto distinto. Lo scaffold appropriato è associato ai prodotti da:

* percorso
* il prodotto può fare riferimento allo scaffold

>[!NOTE]
>
>Il negozio Geometrixx-Outdoors ha un unico tipo di prodotto (e quindi un&#39;unica impalcatura):
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Il tipo di prodotto Geometrixx-Outdoors è attivo su:
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>Puoi creare una definizione di prodotto ovunque sotto senza alcuna configurazione aggiuntiva.

### Importazione prodotti {#importing-products}

#### Importazione prodotti - Interfaccia utente ottimizzata per il tocco {#importing-products-touch-optimized-ui}

1. Accedi a **Prodotti** console, tramite **Commerce**.
1. Utilizzo di **Prodotti** console passa alla posizione desiderata.
1. Utilizza il **Importa prodotti** per aprire la procedura guidata.

   ![Icona Importa prodotti](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Specifica:

   * **Importazione**

     L&#39;importatore per il [fornitore commerce](/help/commerce/cif-classic/administering/concepts.md#commerce-providers), per impostazione predefinita `Geometrixx`.

   * **Origine**

     Il file che desideri importare; puoi utilizzare il browser per selezionare un file.

   * **Importazione incrementale**

     Indica se si tratta di un’importazione incrementale (anziché completa).

   >[!NOTE]
   >
   >L’importazione incrementale (dell’importatore geometrixx-outdoor del campione) opera a livello del prodotto.
   >
   >Un modulo di importazione personalizzato può essere definito per funzionare come richiesto.

1. Seleziona **Successivo** per importare i prodotti, viene visualizzato un registro delle azioni eseguite.

   >[!NOTE]
   >
   >I prodotti vengono importati nella posizione corrente o in relazione a essa.

   >[!NOTE]
   >
   >Utilizzo ripetuto di **Successivo** e **Indietro** importa ripetutamente le definizioni dei prodotti. Tuttavia, poiché hanno gli stessi SKU, le informazioni esistenti nell’archivio vengono sovrascritte.

1. Seleziona **Fine** per chiudere la procedura guidata.

#### Importazione prodotti - Interfaccia classica {#importing-products-classic-ui}

1. Utilizzo di **Strumenti** aprire la console **Commerce** cartella.
1. Fai doppio clic per aprire **Importatore prodotto**:

   ![Console per importazione prodotti](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Specifica:

   * **Nome store**

     I prodotti vengono importati in:

     `/etc/commerce/products/<*store name*>/`

   * **Provider commerce**

     L&#39;importazione per [fornitore commerce](/help/commerce/cif-classic/administering/concepts.md#commerce-providers); per impostazione predefinita, Geometrixx.

   * **File origine**

     Posizione nel repository del file che si desidera importare.

   * **Importazione incrementale**

     Indica se si tratta di un’importazione incrementale (anziché completa).

1. Clic **Importa prodotti**.

### Creazione di informazioni sul prodotto {#creating-product-information}

>[!NOTE]
>
>La gestione standard del prodotto è di base, perché il set di prodotti Geometrixx-Outdoors è stato mantenuto di base. La complessità dipende dal prodotto [scaffolding](/help/sites-authoring/scaffolding.md)quindi, con il vostro scaffolding di prodotto è possibile ottenere un editing più sofisticato.

#### Creazione di informazioni di prodotto - Interfaccia utente ottimizzata per il tocco {#creating-product-information-touch-optimized-ui}

1. Utilizzo di **Prodotti** console (tramite **Commerce**) passa alla posizione desiderata.
1. Utilizza il **Crea** per selezionare una delle seguenti opzioni (a seconda della struttura e della posizione):

   * **Crea prodotto**
   * **Crea variante prodotto**

   ![Icona di creazione a forma di segno più](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Viene visualizzata la procedura guidata. Utilizza il **Base** e **Schede prodotto** per inserire [attributi prodotto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) per il nuovo prodotto o variante di prodotto.

   >[!NOTE]
   >
   >**Titolo** e **SKU** sono il minimo necessario per creare un prodotto o una variante.

1. Seleziona **Crea** per salvare le informazioni.

>[!NOTE]
>
>Molti prodotti sono offerti in una gamma di colori e/o dimensioni. Le informazioni sul prodotto di base e sulle relative varianti possono essere gestite dalla **Prodotti** console.
>
>I prodotti e le relative varianti vengono memorizzati come struttura ad albero, le informazioni sul prodotto si trovano in alto, con le varianti al di sotto (questa struttura viene applicata dall’interfaccia utente).

### Modifica delle informazioni di prodotto {#editing-product-information}

>[!NOTE]
>
>Le immagini del prodotto in geometrixx-outdoors sono servite da:
>
>`/etc/commerce/products/...`
>
>Ciò significa che, per impostazione predefinita, sono bloccati dalla [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html), quindi configura in base alle esigenze.

#### Modifica delle informazioni di prodotto - Interfaccia utente ottimizzata per il tocco {#editing-product-information-touch-optimized-ui}

1. Utilizzo di **Prodotti** console (tramite **Commerce**) passare alle informazioni sul prodotto.
1. Utilizzando:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità di selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona la **Visualizza dati prodotto** icona:

   ![icona visualizza dati prodotto - icona informazioni](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Il [attributi prodotto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) vengono visualizzati. Utilizzare **Modifica** e **Fine** per apportare modifiche.

### Visualizzazione dei riferimenti ai prodotti {#showing-product-references}

#### Visualizzazione dei riferimenti di prodotto - Interfaccia utente ottimizzata per il tocco {#showing-product-references-touch-optimized-ui}

1. Utilizzo di **Prodotti** console (tramite **Commerce**) passare alle informazioni sul prodotto.
1. Apri la barra secondaria per Riferimenti con l’icona:

   ![icona a doppia freccia](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Seleziona il prodotto desiderato: la barra secondaria viene aggiornata e mostra i tipi di riferimento disponibili:

   ![console prodotti con riferimenti aperti](/help/sites-administering/assets/chlimage_1-88.png)

1. Tocca o fai clic sul tipo di riferimento (ad esempio, Pagine prodotto) per espandere l’elenco.
1. Seleziona un riferimento specifico per visualizzare le opzioni:

   * Passa a pagina prodotto
   * Modifica pagina prodotto

   ![Pannello di riferimento della console Prodotti](/help/sites-administering/assets/chlimage_1-89.png)

### Cerca prodotti {#search-for-products}

1. Accedi a **Prodotti** console, tramite **Commerce**.
1. Apri la barra secondaria per Ricerca con l’icona:

   ![icona della lente di ingrandimento](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Sono disponibili diversi facet per la ricerca di prodotti. È possibile utilizzare solo uno o più facet per una ricerca. Vengono visualizzati i prodotti trovati:

   ![Dati dei prodotti nella console prodotti](/help/sites-administering/assets/chlimage_1-90.png)

1. Quando si tocca o si fa clic su un prodotto, questo viene aperto. Puoi anche pubblicarlo o visualizzare i dati del prodotto.

#### Estensione della ricerca {#extending-search}

È possibile modificare un facet esistente o aggiungerne di nuovi utilizzando CRXDE Liti:

1. Accedi a:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Ad esempio, puoi modificare le dimensioni visualizzate nella pagina di ricerca del prodotto. Fai clic su `sizegroup` nodo.
1. Clic `items` , quindi fai clic su `propertypredicate` nodo.
1. Puoi modificare i `propertyValues`. Ad esempio, puoi aggiungere XS o XXL oppure rimuovere una dimensione.
1. Clic **Salva tutto** e passa alla pagina di ricerca prodotti. Le modifiche verranno visualizzate.

### Risorse multiple {#multiple-assets}

Puoi aggiungere più risorse al componente prodotto, quindi specificare la risorsa da visualizzare nella pagina del prodotto.

>[!NOTE]
>
>Tutto ciò che riguarda più risorse viene eseguito con l’interfaccia utente ottimizzata per il tocco.

#### Aggiunta di più risorse {#adding-multiple-assets}

1. Accedi a **Prodotti** console, tramite **Commerce**.
1. Utilizzo di **Prodotti** , passa al prodotto richiesto.

   >[!NOTE]
   >
   >Devi essere a livello di prodotto, non a livello di variante.

1. Seleziona la **Visualizza dati prodotto** con modalità di selezione o azioni rapide.
1. Seleziona l’icona Modifica.
1. Scorri fino a **Aggiungi**.

   ![Aggiunta della schermata dei dati del prodotto](/help/sites-administering/assets/chlimage_1-91.png)

1. Seleziona **Aggiungi**. Viene visualizzato un nuovo segnaposto per la risorsa.
1. Selezione **Cambia** apre una finestra di dialogo che consente di scegliere una risorsa.
1. Seleziona la risorsa da aggiungere.

   >[!NOTE]
   >
   >Le risorse selezionabili sono [Risorse](/help/assets/assets.md).

1. Seleziona l’icona Fine.

Nel componente del prodotto sono ora memorizzate due risorse. Puoi configurare quale viene visualizzato nella pagina del prodotto. Questo funziona con un sistema di categorie. Innanzitutto devi aggiungere una categoria alle singole risorse:

1. Seleziona **Visualizza dati prodotto**.
1. Digita un **Categoria risorsa** sotto le risorse, ad esempio `cat1` e `cat2`.

   >[!NOTE]
   >
   >Puoi anche utilizzare i tag per le categorie.

1. Seleziona l’icona Fine. Ora devi [rollout](#rolling-out-a-catalog) le tue modifiche.

Ora le risorse nel componente prodotto hanno una categoria. Puoi configurare la categoria da visualizzare a tre diversi livelli:

* [Pagina prodotto](#product-page)
* [Catalogo](#catalog)
* [Console Prodotti](#products-console)

>[!NOTE]
>
>Se non imposti categorie, la prima risorsa viene visualizzata nella pagina del prodotto.

Il meccanismo di selezione dell&#39;immagine da visualizzare è il seguente:

1. Verifica se è impostata una categoria per la pagina di prodotto.
1. In caso contrario, verifica se è impostata una categoria per il catalogo.
1. In caso contrario, verifica se è impostata una categoria per la console Prodotti.

>[!NOTE]
>
>Per applicare le modifiche e visualizzare la differenza nella pagina del prodotto, è necessario eseguire il rollout delle modifiche sia a livello di catalogo che a livello di console prodotti.

#### Pagina prodotto {#product-page}

1. Passa alla pagina del prodotto.
1. **Modifica** il componente prodotto.
1. Digita il **Categoria immagine** che hai scelto ( `cat1` ad esempio).
1. Seleziona **Fine**. La pagina viene aggiornata e viene visualizzata la risorsa corretta.

#### Catalogo  {#catalog}

1. Passa al catalogo.
1. Seleziona **Visualizza proprietà**.
1. Seleziona **Modifica**.
1. Seleziona la **Risorse** scheda.
1. Digita il valore richiesto **Categoria risorse di prodotto**.
1. Seleziona **Fine**.
1. [Rollout](#rolling-out-a-catalog) le tue modifiche.

#### Console Prodotti {#products-console}

1. Utilizzo di **Prodotti** , passare al Prodotto richiesto.
1. Seleziona **Visualizza dati prodotto**.
1. Seleziona **Modifica**.
1. Digita un **Categoria risorsa predefinita**.
1. Seleziona **Fine**.
1. [Rollout](#rolling-out-a-catalog) le tue modifiche.

### Pubblicazione/Annullamento della pubblicazione delle informazioni di prodotto {#publishing-unpublishing-product-information}

#### Pubblicazione/Annullamento della pubblicazione delle informazioni di prodotto - Interfaccia utente ottimizzata per il tocco {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>Spesso le informazioni sul prodotto vengono pubblicate attraverso le pagine che vi fanno riferimento. Ad esempio, quando pubblichi la pagina X che fa riferimento al prodotto Y, l’AEM ti chiede se desideri pubblicare anche il prodotto Y.
>
>Per casi speciali, l’AEM supporta anche la pubblicazione diretta dai dati dei prodotti.

1. Utilizzo di **Prodotti** console (tramite **Commerce**) passare alle informazioni sul prodotto.
1. Utilizzando:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità di selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona la **Pubblica** o **Annulla pubblicazione** icona come richiesto:

   ![icona mondo](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![icona del mondo con una croce - nessun segno](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   Le informazioni sul prodotto sono pubblicate o non pubblicate, a seconda dei casi.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### Gestore eventi per aggiornamenti prodotto {#event-handler-for-product-updates}

È disponibile un Gestore eventi che registra un evento quando un prodotto viene aggiunto, modificato o eliminato e quando una pagina di prodotto viene aggiunta, modificata o eliminata. Sono disponibili i seguenti eventi OSGi:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

Per `PRODUCT_*` eventi, il percorso punta al prodotto di base in `/etc/commerce/products`. Per `PRODUCT_PAGE_*` eventi, il percorso punta al `cq:Page` nodo.

Puoi visualizzarli nella console web in eventi OSGI ( `/system/console/events`), ad esempio:

![Esempi di eventi OSGI](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Leggi anche [Gestione degli eventi nell’AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### Immagine con collegamenti Aggiungi al carrello {#image-with-add-to-cart-links}

Il componente Immagine con collegamenti Aggiungi al carrello consente di aggiungere rapidamente un prodotto al carrello creando un hotspot collegato a un prodotto su un’immagine.

Facendo clic sul punto attivo viene aperta una finestra di dialogo che consente di scegliere le dimensioni e la quantità del prodotto.

1. Passa alla pagina in cui desideri aggiungere il componente.
1. Trascina e rilascia il componente nella pagina.
1. Trascina e rilascia un’immagine nel componente da [browser risorse](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Puoi effettuare le seguenti operazioni:

   * fai clic sul componente, quindi sull’icona Modifica
   * fare un doppio clic lento

1. Fai clic sull’icona a schermo intero.

   ![icona a schermo intero](/help/sites-administering/assets/chlimage_1-92.png)

1. Fai clic sull’icona Launch Map.

   ![icona mappa di lancio](/help/sites-administering/assets/chlimage_1-93.png)

1. Fare clic su una delle icone delle forme.

   ![icone delle forme](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Modificare e spostare la forma in base alle esigenze.
1. Fare clic sulla forma.
1. Facendo clic sull&#39;icona Sfoglia si apre [Selettore risorse](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >In alternativa, puoi digitare direttamente il percorso del prodotto che deve essere a livello di prodotto, non a livello di variante.

   ![digita percorso](/help/sites-administering/assets/chlimage_1-94.png)

1. Fai clic due volte sull&#39;icona di conferma, quindi fai clic su esci da schermo intero.
1. Fai clic in un punto della pagina accanto al componente. La pagina deve essere aggiornata e sull&#39;immagine dovrebbe essere visualizzato il simbolo seguente:

   ![simbolo più](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Passa a [anteprima](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) modalità.
1. Fai clic sul punto attivo +. Viene visualizzata una finestra di dialogo in cui è possibile scegliere le dimensioni e la quantità del prodotto immesso **Percorso**.

   ![esempio di prodotto: poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. Inserire una dimensione e una quantità.
1. Fai clic sul pulsante Aggiungi al carrello. La finestra di dialogo si chiude.
1. Passa al carrello. Il prodotto dovrebbe essere qui.

#### Opzioni di configurazione {#configuration-options}

Puoi configurare l’aspetto della finestra di dialogo quando fai clic sul punto attivo:

1. Fai clic sul componente e sull’icona Configura.

   ![icona configura](/help/sites-administering/assets/chlimage_1-96.png)

1. Scorri verso il basso. È presente un **AGGIUNGI AL CARRELLO** scheda.

   ![scheda aggiungi al carrello](/help/sites-administering/assets/chlimage_1-97.png)

1. Clic **AGGIUNGI AL CARRELLO**. È possibile utilizzare tre opzioni di configurazione.

   ![opzioni di configurazione](/help/sites-administering/assets/chlimage_1-98.png)

1. Fai clic sull’icona Fine.

## Cataloghi {#catalogs}

### Generazione di un catalogo {#generating-a-catalog}

#### Generazione di un catalogo - Interfaccia utente ottimizzata per il tocco {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>Il catalogo fa riferimento ai dati di prodotto.

Per generare un catalogo:

1. Apri la console Sites (ad esempio, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Passa alla posizione in cui desideri creare la pagina.
1. Per aprire l&#39;elenco di opzioni, utilizzare **Crea** icona:

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. Dall’elenco, seleziona **Crea catalogo**. Viene visualizzata la procedura guidata Crea catalogo.

   ![creazione guidata catalogo](/help/sites-administering/assets/chlimage_1-99.png)

1. Passa alla blueprint del catalogo richiesta.
1. Seleziona la **Seleziona** e tocca o fai clic sulla blueprint del catalogo richiesta.
1. Seleziona **Avanti**.

   ![creazione guidata proprietà catalogo](/help/sites-administering/assets/chlimage_1-100.png)

1. Digita un **Titolo** e un **Nome**.
1. Seleziona il pulante **Crea.** Viene creato il catalogo e viene visualizzata una finestra di dialogo.

   ![finestra di dialogo per creazione catalogo](/help/sites-administering/assets/chlimage_1-101.png)

1. Selezione del **Fine** ti riporta alla console Sites, dove puoi visualizzare il catalogo.

   Tocco/clic **Apri catalogo** apre il catalogo (ad esempio `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Generazione di un catalogo - Interfaccia classica {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>Il catalogo fa riferimento al tuo [Dati prodotto](#products-and-product-variants).

1. Utilizzo di **Siti Web** , passare alla **Blueprint catalogo**, quindi il Catalogo base.

   Ad esempio:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Creare una pagina utilizzando **Blueprint sezione** modello.

   Esempio: `Swimwear`.

1. Apri il nuovo `Swimwear` , quindi fai clic su **Modifica blueprint**. Il **Proprietà** viene visualizzata una finestra di dialogo che consente di impostare **Prodotti** selezione.

   Ad esempio, apri il **Tag/Parole chiave** per selezionare Attività, quindi Nuoto dalla sezione Geometrixx all&#39;aperto.

1. Clic **OK** in modo che le proprietà vengano salvate; i prodotti di esempio vengono visualizzati sotto **Criteri di selezione del prodotto** nella pagina blueprint.
1. Clic **Modifiche rollout...**, seleziona **Rollout pagina e tutte le relative sottopagine**, quindi fai clic su **Successivo** allora **Rollout**. Una volta completato correttamente il rollout, **Stato** L&#39;indicatore viene visualizzato in verde.
1. Ora puoi fare clic su **Chiudi** e controlla la nuova sezione del catalogo; ad esempio, in e in:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. Di nuovo dalla pagina blueprint fai clic su **Modifica blueprint** e nella **Proprietà** apri la finestra di dialogo **Pagina generata** scheda. Nel campo Elenco banner selezionare l&#39;immagine che si desidera visualizzare, ad esempio: `summer.jpg`
1. Clic **OK** in modo che le proprietà vengano salvate; le informazioni del banner vengono visualizzate sotto **Criteri di selezione del prodotto** nella pagina blueprint.
1. Effettua il rollout delle nuove modifiche.

### Rollout di un catalogo {#rolling-out-a-catalog}

#### Rollout di un catalogo - Interfaccia touch {#rolling-out-a-catalog-touch-optimized-ui}

Per eseguire il rollout di un catalogo:

1. Accedi a **Cataloghi** console, tramite **Commerce**.
1. Passa al catalogo di cui desideri eseguire il rollout.
1. Utilizzando:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità di selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona la **Modifiche rollout** icona:

   ![rollout](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. Nella procedura guidata, imposta il rollout in base alle esigenze, quindi tocca o fai clic su **Modifiche rollout**.
1. Viene visualizzata una finestra di dialogo. Seleziona **Fine** al termine del processo.

#### Rollout di un catalogo - Interfaccia classica {#rolling-out-a-catalog-classic-ui}

Per eseguire il rollout di un catalogo:

1. Passa al catalogo di cui desideri eseguire il rollout. Ad esempio:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Clic **Modifiche rollout...**
1. Imposta il rollout in base alle esigenze.
1. Clic **Rollout**.

### Importazione blueprint {#blueprint-importer}

#### Importazione blueprint - Interfaccia utente ottimizzata per il tocco {#blueprint-importer-touch-optimized-ui}

1. Accedi a **Cataloghi** console, tramite **Commerce**.
1. Passa alla posizione in cui desideri importare la blueprint del catalogo.
1. Seleziona la **Importa blueprint** icona.

   ![Icona Importa blueprint](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Nella procedura guidata, seleziona l’Origine desiderata e tocca o fai clic su **Successivo**.

   ![procedura guidata blueprint](/help/sites-administering/assets/chlimage_1-102.png)

1. Seleziona **Fine** al termine dell’importazione.

#### Importazione blueprint - Interfaccia classica {#blueprint-importer-classic-ui}

1. Utilizzo di **Strumenti** , passa a **Commerce**.

   Ad esempio:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Apri **Importazione bluprint catalogo**.
1. Imposta l’importazione in base alle esigenze.
1. Clic **Importa blueprint catalogo**.

## Promozioni {#promotions}

### Creazione di una promozione {#creating-a-promotion}

#### Creazione di una promozione - Interfaccia classica {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>L’esempio seguente riguarda una promozione detenuta direttamente in un [campagna](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), viene utilizzato per i voucher.
>
>Una promozione può essere anche in un [esperienza](/help/sites-authoring/personalization.md) all’interno di una campagna.
>
>Per ulteriori informazioni, consulta [Promozioni e voucher](#promotions-and-vouchers).

1. Apri **Siti Web** dell’istanza Autore.
1. Nel riquadro a sinistra, selezionare il **Campagna**.
1. Clic **Nuovo**, seleziona la **Promozione** , quindi specifica un **Titolo** (e **Nome** se necessario) per il nuovo voucher.
1. Fai clic su **Crea**. La nuova pagina della promozione viene visualizzata nel riquadro di destra.

1. Modifica il **Proprietà** mediante:

   * aprire la pagina, quindi fare clic sul pulsante Modifica per aprire la finestra di dialogo Proprietà
   * selezionando la pagina nella console Siti Web, quindi utilizzando il menu di scelta rapida (in genere il pulsante destro del mouse) per selezionare **Proprietà...** e apri la finestra di dialogo proprietà

   Specifica la **Tipo di promozione**, **Tipo di sconto**, **Valore sconto** e qualsiasi altro campo richiesto.

1. Clic **OK** per salvare.

1. Ora puoi attivare la promozione in modo che gli acquirenti possano visualizzarla nell’istanza Publish.

## Voucher {#vouchers}

### Creazione di un voucher {#creating-a-voucher}

#### Creazione di un voucher - Interfaccia classica {#creating-a-voucher-classic-ui}

1. Apri **Siti Web** dell’istanza Autore.
1. Nel riquadro a sinistra, selezionare il **Campagna**.
1. Clic **Nuovo**, seleziona la **Voucher** , quindi specifica un **Titolo** (e **Nome** se necessario) per il nuovo voucher.
1. Fai clic su **Crea**. La nuova pagina del voucher viene visualizzata nel riquadro di destra.

1. Apri la nuova pagina del voucher con un doppio clic, quindi fai clic su **Modifica** e configura le informazioni come richiesto.
1. Clic **OK** per salvare.

1. Ora puoi attivare il voucher, in modo che gli acquirenti possano utilizzarlo nei loro carrelli sull’istanza Publish.

### Rimozione dei voucher {#removing-vouchers}

#### Rimozione dei voucher - Interfaccia classica {#removing-vouchers-classic-ui}

Per rendere un voucher non disponibile ai clienti, puoi effettuare le seguenti operazioni:

* Disattiva il voucher: rimane disponibile nell’ambiente di authoring per poterlo riattivare in un secondo momento.
* Eliminalo completamente.

Entrambe le azioni possono essere eseguite dalla **Siti Web** console.

### Modifica dei voucher {#modifying-vouchers}

#### Modifica dei voucher - Interfaccia classica {#modifying-vouchers-classic-ui}

Per modificare le proprietà di un voucher o di una promozione, è possibile fare doppio clic su di esso nel **Siti Web** e fai clic su **Modifica**. Dopo averlo salvato, devi attivarlo in modo che le modifiche vengano inviate alle istanze di pubblicazione.

### Aggiunta di voucher a un carrello {#adding-vouchers-to-a-cart}

Per consentire agli utenti di aggiungere voucher ai loro carrelli, puoi utilizzare il **Voucher** componente (categoria Commerce). Aggiungilo alla stessa pagina in cui viene visualizzato il carrello (ma questo non è obbligatorio). Il componente voucher è semplicemente un modulo in cui l’utente può immettere un codice voucher; è il componente carrello che mostra effettivamente l’elenco dei voucher applicati e il relativo sconto.

Nel sito demo (Geometrixx Outdoors - inglese) puoi vedere il modulo del voucher nella pagina del carrello, sotto il carrello effettivo.

## Ordini {#orders}

>[!NOTE]
>
>È opportuno ricordare che l’AEM preconfigurato non prevede azioni necessarie per le funzionalità standard relative agli ordini, come la restituzione delle merci, l’aggiornamento dello stato degli ordini, l’evasione, la generazione dei documenti di trasporto. Si tratta principalmente di un’anteprima tecnologica.
>
>La gestione ordini generica in AEM è stata mantenuta di base; i campi disponibili nella procedura guidata dipendono dallo scaffold:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>Se si crea uno scaffold personalizzato, è possibile memorizzare ulteriori informazioni sull&#39;ordine.

>[!NOTE]
>
>La console Ordini espone le informazioni sugli ordini dei fornitori, che non vengono mai pubblicate.
>
>Le informazioni sull&#39;ordine del cliente vengono conservate nelle directory principali e sono esposte dalla cronologia dell&#39;ordine per il relativo account. Queste informazioni vengono pubblicate insieme al resto della home directory.

### Creazione di informazioni sull&#39;ordine {#creating-order-information}

#### Creazione di informazioni sull’ordine - Interfaccia utente ottimizzata per il tocco {#creating-order-information-touch-optimized-ui}

1. Utilizzo di **Ordini** console passa alla posizione desiderata.
1. Utilizza il **Crea** icona per selezionare **Crea ordine**.

   ![Icona di creazione a forma di segno più](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Viene visualizzata la procedura guidata. Utilizza il **Base**, **Contenuto**, **Pagamento**, e **Evasione** schede per inserire [informazioni sul nuovo ordine](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Seleziona **Crea** per salvare le informazioni.

### Modifica delle informazioni dell&#39;ordine {#editing-order-information}

#### Modifica delle informazioni sull’ordine - Interfaccia utente ottimizzata per il tocco {#editing-order-information-touch-optimized-ui}

1. Utilizzo di **Ordini** console passa all’ordine.
1. Utilizzando:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità di selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona la **Visualizza dati ordine** icona:

   ![icona informazioni](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Il [informazioni ordine](/help/commerce/cif-classic/administering/concepts.md#order-information) viene visualizzato. Utilizzare **Modifica** e **Fine** per apportare modifiche.

