---
title: Amministrazione di eCommerce generico
description: La soluzione generica dell’AEM fornisce metodi per gestire le informazioni commerciali contenute nell’archivio.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2907'
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

Prima di creare i prodotti, definire uno scaffold [&#128279;](/help/sites-authoring/scaffolding.md). Specifica i campi da definire, i prodotti e la modalità di modifica.

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

1. Passa alla console **Prodotti** tramite **Commerce**.
1. Utilizzando la console **Prodotti**, passa alla posizione desiderata.
1. Utilizza l&#39;icona **Importa prodotti** per aprire la procedura guidata.

   ![Icona Importa prodotti](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Specifica:

   * **Importazione**

     L&#39;importazione per il provider commerce [specifico](/help/commerce/cif-classic/administering/concepts.md#commerce-providers), per impostazione predefinita `Geometrixx`.

   * **Origine**

     Il file che desideri importare; puoi utilizzare il browser per selezionare un file.

   * **Importazione incrementale**

     Indica se si tratta di un’importazione incrementale (anziché completa).

   >[!NOTE]
   >
   >L’importazione incrementale (dell’importatore geometrixx-outdoor del campione) opera a livello del prodotto.
   >
   >Un modulo di importazione personalizzato può essere definito per funzionare come richiesto.

1. Seleziona **Avanti** per importare i prodotti, viene visualizzato un registro delle azioni eseguite.

   >[!NOTE]
   >
   >I prodotti vengono importati nella posizione corrente o in relazione a essa.

   >[!NOTE]
   >
   >Usando ripetutamente **Avanti** e **Indietro** importa ripetutamente le definizioni dei prodotti. Tuttavia, poiché hanno gli stessi SKU, le informazioni esistenti nell’archivio vengono sovrascritte.

1. Seleziona **Fine** per chiudere la procedura guidata.

#### Importazione prodotti - Interfaccia classica {#importing-products-classic-ui}

1. Utilizzando la console **Strumenti**, apri la cartella **Commerce**.
1. Fai doppio clic per aprire **Importazione prodotti**:

   ![Console Importazione Prodotti](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Specifica:

   * **Nome archivio**

     I prodotti vengono importati in:

     `/etc/commerce/products/<*store name*>/`

   * **Provider Commerce**

     L&#39;importazione per il tuo [provider commerce](/help/commerce/cif-classic/administering/concepts.md#commerce-providers); per impostazione predefinita, Geometrixx.

   * **File Source**

     Posizione nel repository del file che si desidera importare.

   * **Importazione incrementale**

     Indica se si tratta di un’importazione incrementale (anziché completa).

1. Fai clic su **Importa prodotti**.

### Creazione di informazioni sul prodotto {#creating-product-information}

>[!NOTE]
>
>La gestione standard del prodotto è di base, perché il set di prodotti Geometrixx-Outdoors è stato mantenuto di base. La complessità si basa sullo scaffolding [del prodotto](/help/sites-authoring/scaffolding.md), quindi con lo scaffolding del tuo prodotto puoi ottenere modifiche più sofisticate.

#### Creazione di informazioni di prodotto - Interfaccia utente ottimizzata per il tocco {#creating-product-information-touch-optimized-ui}

1. Utilizzando la console **Prodotti** (tramite **Commerce**) passa alla posizione desiderata.
1. Utilizza l&#39;icona **Crea** per selezionare (a seconda della struttura e del percorso):

   * **Crea prodotto**
   * **Crea variante prodotto**

   ![Icona di creazione a forma di segno più](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Viene visualizzata la procedura guidata. Utilizza le **Schede base** e **Schede prodotto** per immettere gli [attributi prodotto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) per il nuovo prodotto o la nuova variante prodotto.

   >[!NOTE]
   >
   >Per creare un prodotto o una variante sono necessari almeno **Title** e **SKU**.

1. Seleziona **Crea** per salvare le informazioni.

>[!NOTE]
>
>Molti prodotti sono offerti in una gamma di colori e/o dimensioni. Le informazioni sul prodotto di base e sulle relative varianti possono essere gestite dalla console **Prodotti**.
>
>I prodotti e le relative varianti vengono memorizzati come struttura ad albero, le informazioni sul prodotto si trovano in alto, con le varianti al di sotto (questa struttura viene applicata dall’interfaccia utente).

### Modifica delle informazioni di prodotto {#editing-product-information}

>[!NOTE]
>
>Le immagini del prodotto in geometrixx-outdoors sono servite da:
>
>`/etc/commerce/products/...`
>
>Ciò significa che, per impostazione predefinita, sono bloccati da [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=it), quindi configura come richiesto.

#### Modifica delle informazioni di prodotto - Interfaccia utente ottimizzata per il tocco {#editing-product-information-touch-optimized-ui}

1. Utilizzando la console **Prodotti** (tramite **Commerce**) passa alle informazioni sul prodotto.
1. Utilizzando:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità di selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona l&#39;icona **Visualizza dati prodotto**:

   ![icona visualizza dati prodotto - icona informazioni](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Vengono visualizzati [attributi prodotto](/help/commerce/cif-classic/administering/concepts.md#product-attributes). Utilizza **Modifica** e **Fine** per apportare modifiche.

### Visualizzazione dei riferimenti ai prodotti {#showing-product-references}

#### Visualizzazione dei riferimenti di prodotto - Interfaccia utente ottimizzata per il tocco {#showing-product-references-touch-optimized-ui}

1. Utilizzando la console **Prodotti** (tramite **Commerce**) passa alle informazioni sul prodotto.
1. Apri la barra secondaria per Riferimenti con l’icona:

   ![icona a forma di doppia freccia](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Seleziona il prodotto desiderato: la barra secondaria viene aggiornata e mostra i tipi di riferimento disponibili:

   Console ![prodotti con riferimenti aperti](/help/sites-administering/assets/chlimage_1-88.png)

1. Fai clic sul tipo di riferimento (ad esempio, Pagine prodotto) per espandere l’elenco.
1. Seleziona un riferimento specifico per visualizzare le opzioni:

   * Passa a pagina prodotto
   * Modifica pagina prodotto

   ![Pannello di riferimento della console Prodotti](/help/sites-administering/assets/chlimage_1-89.png)

### Cerca prodotti {#search-for-products}

1. Passa alla console **Prodotti** tramite **Commerce**.
1. Apri la barra secondaria per Ricerca con l’icona:

   ![icona della lente d&#39;ingrandimento](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Sono disponibili diversi facet per la ricerca di prodotti. È possibile utilizzare solo uno o più facet per una ricerca. Vengono visualizzati i prodotti trovati:

   ![Dati prodotto nella console prodotti](/help/sites-administering/assets/chlimage_1-90.png)

1. Quando si tocca o si fa clic su un prodotto, questo viene aperto. Puoi anche pubblicarlo o visualizzare i dati del prodotto.

#### Estensione della ricerca {#extending-search}

È possibile modificare un facet esistente o aggiungerne di nuovi utilizzando CRXDE Lite:

1. Accedi a:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Ad esempio, puoi modificare le dimensioni visualizzate nella pagina di ricerca del prodotto. Fare clic sul nodo `sizegroup`.
1. Fare clic su `items` nodo, quindi su `propertypredicate` nodo.
1. È possibile modificare `propertyValues`. Ad esempio, puoi aggiungere XS o XXL oppure rimuovere una dimensione.
1. Fai clic su **Salva tutto** e passa alla pagina di ricerca prodotti. Le modifiche verranno visualizzate.

### Più Assets {#multiple-assets}

Puoi aggiungere più risorse al componente prodotto, quindi specificare la risorsa da visualizzare nella pagina del prodotto.

>[!NOTE]
>
>Tutto ciò che riguarda più risorse viene eseguito con l’interfaccia utente ottimizzata per il tocco.

#### Aggiunta di più Assets {#adding-multiple-assets}

1. Passa alla console **Prodotti** tramite **Commerce**.
1. Utilizzando la console **Prodotti**, passa al prodotto richiesto.

   >[!NOTE]
   >
   >Devi essere a livello di prodotto, non a livello di variante.

1. Seleziona l&#39;icona **Visualizza dati prodotto** con modalità di selezione o azioni rapide.
1. Seleziona l’icona Modifica.
1. Scorri fino a **Aggiungi**.

   ![Aggiunta schermata dati prodotto](/help/sites-administering/assets/chlimage_1-91.png)

1. Seleziona **Aggiungi**. Viene visualizzato un nuovo segnaposto per la risorsa.
1. Selezionando **Modifica** si apre una finestra di dialogo che consente di scegliere una risorsa.
1. Seleziona la risorsa da aggiungere.

   >[!NOTE]
   >
   >Le risorse che puoi selezionare provengono da [Assets](/help/assets/assets.md).

1. Seleziona l’icona Fine.

Nel componente del prodotto sono ora memorizzate due risorse. Puoi configurare quale viene visualizzato nella pagina del prodotto. Questo funziona con un sistema di categorie. Innanzitutto devi aggiungere una categoria alle singole risorse:

1. Selezionare **Visualizza dati prodotto**.
1. Digita una **Categoria risorse** sotto le risorse, ad esempio `cat1` e `cat2`.

   >[!NOTE]
   >
   >Puoi anche utilizzare i tag per le categorie.

1. Seleziona l’icona Fine. Ora devi [eseguire il rollout](#rolling-out-a-catalog) delle modifiche.

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
1. **Modifica** il componente del prodotto.
1. Digitare la **Categoria immagine** scelta ( `cat1`, ad esempio).
1. Seleziona **Fine**. La pagina viene aggiornata e viene visualizzata la risorsa corretta.

#### Catalogo  {#catalog}

1. Passa al catalogo.
1. Selezionare **Visualizza proprietà**.
1. Seleziona **Modifica**.
1. Seleziona la scheda **Risorse**.
1. Digita la **categoria di risorse di prodotto** richiesta.
1. Seleziona **Fine**.
1. [Effettua il rollout](#rolling-out-a-catalog) delle modifiche.

#### Console Prodotti {#products-console}

1. Utilizzando la console **Prodotti**, passa al prodotto richiesto.
1. Selezionare **Visualizza dati prodotto**.
1. Seleziona **Modifica**.
1. Digita una **categoria di risorse predefinita**.
1. Seleziona **Fine**.
1. [Effettua il rollout](#rolling-out-a-catalog) delle modifiche.

### Pubblicazione/Annullamento della pubblicazione delle informazioni di prodotto {#publishing-unpublishing-product-information}

#### Pubblicazione/Annullamento della pubblicazione delle informazioni di prodotto - Interfaccia utente ottimizzata per il tocco {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>Spesso le informazioni sul prodotto vengono pubblicate attraverso le pagine che vi fanno riferimento. Ad esempio, quando pubblichi la pagina X che fa riferimento al prodotto Y, l’AEM ti chiede se desideri pubblicare anche il prodotto Y.
>
>Per casi speciali, l’AEM supporta anche la pubblicazione diretta dai dati dei prodotti.

1. Utilizzando la console **Prodotti** (tramite **Commerce**) passa alle informazioni sul prodotto.
1. Utilizzando:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità di selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona l&#39;icona **Publish** o **Annulla pubblicazione** come richiesto:

   ![icona mondo](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![icona mondo con croce - nessun segno](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   Le informazioni sul prodotto sono pubblicate o non pubblicate, a seconda dei casi.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
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

Per gli eventi `PRODUCT_*`, il percorso punta al prodotto di base in `/etc/commerce/products`. Per gli eventi `PRODUCT_PAGE_*`, il percorso punta al nodo `cq:Page`.

È possibile visualizzarli nella console Web in eventi OSGI ( `/system/console/events`), ad esempio:

![Esempi di eventi OSGI](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Leggi anche [Gestione degli eventi in AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### Immagine con collegamenti Aggiungi al carrello {#image-with-add-to-cart-links}

Il componente Immagine con collegamenti Aggiungi al carrello consente di aggiungere rapidamente un prodotto al carrello creando un hotspot collegato a un prodotto su un’immagine.

Facendo clic sul punto attivo viene aperta una finestra di dialogo che consente di scegliere le dimensioni e la quantità del prodotto.

1. Passa alla pagina in cui desideri aggiungere il componente.
1. Trascina e rilascia il componente nella pagina.
1. Trascina un&#39;immagine nel componente dal browser [risorse](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Puoi effettuare le seguenti operazioni:

   * fai clic sul componente, quindi sull’icona Modifica
   * fare un doppio clic lento

1. Fai clic sull’icona a schermo intero.

   ![icona a schermo intero](/help/sites-administering/assets/chlimage_1-92.png)

1. Fai clic sull’icona Launch Map.

   ![icona mappa di avvio](/help/sites-administering/assets/chlimage_1-93.png)

1. Fare clic su una delle icone delle forme.

   ![icone forma](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Modificare e spostare la forma in base alle esigenze.
1. Fare clic sulla forma.
1. Facendo clic sull&#39;icona Sfoglia si apre [il selettore risorse](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >In alternativa, puoi digitare direttamente il percorso del prodotto che deve essere a livello di prodotto, non a livello di variante.

   ![percorso tipo](/help/sites-administering/assets/chlimage_1-94.png)

1. Fai clic due volte sull&#39;icona di conferma, quindi fai clic su esci da schermo intero.
1. Fai clic in un punto della pagina accanto al componente. La pagina deve essere aggiornata e sull&#39;immagine dovrebbe essere visualizzato il simbolo seguente:

   ![simbolo più](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Passa alla modalità [anteprima](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui).
1. Fai clic sul punto attivo +. Viene visualizzata una finestra di dialogo in cui è possibile scegliere le dimensioni e la quantità del prodotto immesso in **Percorso**.

   ![esempio di prodotto: poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. Inserire una dimensione e una quantità.
1. Fai clic sul pulsante Aggiungi al carrello. La finestra di dialogo si chiude.
1. Passa al carrello. Il prodotto dovrebbe essere qui.

#### Opzioni di configurazione {#configuration-options}

Puoi configurare l’aspetto della finestra di dialogo quando fai clic sul punto attivo:

1. Fai clic sul componente e sull’icona Configura.

   ![icona di configurazione](/help/sites-administering/assets/chlimage_1-96.png)

1. Scorri verso il basso. Scheda **AGGIUNGI AL CARRELLO**.

   ![aggiungi alla scheda carrello](/help/sites-administering/assets/chlimage_1-97.png)

1. Fai clic su **AGGIUNGI AL CARRELLO**. È possibile utilizzare tre opzioni di configurazione.

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
1. Per aprire l&#39;elenco di opzioni, utilizzare l&#39;icona **Crea**:

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. Dall&#39;elenco, selezionare **Crea catalogo**. Viene visualizzata la procedura guidata Crea catalogo.

   ![creazione guidata catalogo](/help/sites-administering/assets/chlimage_1-99.png)

1. Passa alla blueprint del catalogo richiesta.
1. Seleziona il pulsante **Seleziona** e fai clic sulla blueprint del catalogo richiesta.
1. Seleziona **Avanti**.

   ![creazione guidata proprietà catalogo](/help/sites-administering/assets/chlimage_1-100.png)

1. Digita un **Titolo** e un **Nome**.
1. Seleziona il pulsante **Crea**. Viene creato il catalogo e viene visualizzata una finestra di dialogo.

   ![finestra di dialogo di creazione del catalogo](/help/sites-administering/assets/chlimage_1-101.png)

1. Se selezioni il pulsante **Fine**, torni alla console Sites dove puoi visualizzare il catalogo.

   Toccando/facendo clic sul pulsante **Apri catalogo** si apre il catalogo (ad esempio, `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Generazione di un catalogo - Interfaccia classica {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>Il catalogo fa riferimento ai tuoi [dati prodotto](#products-and-product-variants).

1. Utilizzando la console **Siti Web**, passa a **Blueprint catalogo**, quindi al Catalogo base.

   Ad esempio:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Crea una pagina utilizzando il modello **Blueprint sezione**.

   Esempio: `Swimwear`.

1. Apri la nuova pagina `Swimwear`, quindi fai clic su **Modifica blueprint**. Viene visualizzata la finestra di dialogo **Proprietà** che consente di impostare la selezione di **Prodotti**.

   Apri ad esempio il campo **Tag/Parole chiave** per selezionare Attività, quindi Nuoto dalla sezione Geometrixx all&#39;aperto.

1. Fai clic su **OK** per salvare le proprietà; i prodotti di esempio vengono visualizzati in **Criteri di selezione prodotto** nella pagina blueprint.
1. Fai clic su **Rollout modifiche...**, seleziona **Rollout pagina e tutte le sottopagine**, quindi fai clic su **Avanti** e poi su **Rollout**. Una volta completato correttamente il rollout, l&#39;indicatore **Stato** viene visualizzato in verde.
1. Ora puoi fare clic su **Chiudi** e controllare la nuova sezione del catalogo; ad esempio, in e in:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. Di nuovo dalla pagina blueprint fai clic su **Modifica blueprint** e nella finestra di dialogo **Proprietà** apri la scheda **Pagina generata**. Nel campo Elenco banner selezionare l&#39;immagine che si desidera visualizzare, ad esempio `summer.jpg`
1. Fai clic su **OK** per salvare le proprietà; le informazioni del banner vengono visualizzate in **Criteri di selezione prodotto** nella pagina blueprint.
1. Effettua il rollout delle nuove modifiche.

### Rollout di un catalogo {#rolling-out-a-catalog}

#### Rollout di un catalogo - Interfaccia touch {#rolling-out-a-catalog-touch-optimized-ui}

Per eseguire il rollout di un catalogo:

1. Passa alla console **Cataloghi** tramite **Commerce**.
1. Passa al catalogo di cui desideri eseguire il rollout.
1. Utilizzando:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità di selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona l&#39;icona **Rollout modifiche**:

   ![rollout](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. Nella procedura guidata, imposta il rollout come necessario, quindi fai clic su **Rollout modifiche**.
1. Viene visualizzata una finestra di dialogo. Seleziona **Fine** al termine del processo.

#### Rollout di un catalogo - Interfaccia classica {#rolling-out-a-catalog-classic-ui}

Per eseguire il rollout di un catalogo:

1. Passa al catalogo di cui desideri eseguire il rollout. Ad esempio:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Fai clic su **Rollout modifiche...**
1. Imposta il rollout in base alle esigenze.
1. Fai clic su **Rollout**.

### Importazione blueprint {#blueprint-importer}

#### Importazione blueprint - Interfaccia utente ottimizzata per il tocco {#blueprint-importer-touch-optimized-ui}

1. Passa alla console **Cataloghi** tramite **Commerce**.
1. Passa alla posizione in cui desideri importare la blueprint del catalogo.
1. Seleziona l&#39;icona **Importa blueprint**.

   ![Icona Importa blueprint](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Nella procedura guidata, seleziona il Source come richiesto e fai clic su **Avanti**.

   ![procedura guidata blueprint](/help/sites-administering/assets/chlimage_1-102.png)

1. Seleziona **Fine** al termine dell&#39;importazione.

#### Importazione blueprint - Interfaccia classica {#blueprint-importer-classic-ui}

1. Utilizzando la console **Strumenti**, passa a **Commerce**.

   Ad esempio:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Apri **Importazione blueprint catalogo**.
1. Imposta l’importazione in base alle esigenze.
1. Fai clic su **Importa blueprint catalogo**.

## Promozioni {#promotions}

### Creazione di una promozione {#creating-a-promotion}

#### Creazione di una promozione - Interfaccia classica {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>L&#39;esempio seguente riguarda una promozione detenuta direttamente in una [campagna](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), che viene utilizzata per i voucher.
>
>Una promozione può trovarsi anche in una [esperienza](/help/sites-authoring/personalization.md) all&#39;interno di una campagna.
>
>Per ulteriori informazioni, consulta [Promozioni e voucher](#promotions-and-vouchers).

1. Apri la console **Siti Web** dell&#39;istanza Autore.
1. Nel riquadro a sinistra, seleziona la **Campagna** richiesta.
1. Fai clic su **Nuovo**, seleziona il modello **Promozione**, quindi specifica un **Titolo** (e **Nome** se necessario) per il nuovo voucher.
1. Fai clic su **Crea**. La nuova pagina della promozione viene visualizzata nel riquadro di destra.

1. Modifica le **proprietà** in uno dei modi seguenti:

   * aprire la pagina, quindi fare clic sul pulsante Modifica per aprire la finestra di dialogo Proprietà
   * selezionando la pagina nella console Siti Web, quindi utilizzando il menu di scelta rapida (in genere il pulsante destro del mouse) per selezionare **Proprietà...** e aprire la finestra di dialogo delle proprietà

   Specifica il **Tipo promozione**, il **Tipo sconto**, il **Valore sconto** ed eventuali altri campi come richiesto.

1. Fare clic su **OK** per salvare.

1. Ora puoi attivare la promozione in modo che gli acquirenti possano visualizzarla nell’istanza Publish.

## Voucher {#vouchers}

### Creazione di un voucher {#creating-a-voucher}

#### Creazione di un voucher - Interfaccia classica {#creating-a-voucher-classic-ui}

1. Apri la console **Siti Web** dell&#39;istanza Autore.
1. Nel riquadro a sinistra, seleziona la **Campagna** richiesta.
1. Fai clic su **Nuovo**, seleziona il modello **Voucher**, quindi specifica un **Titolo** (e **Nome** se necessario) per il nuovo voucher.
1. Fai clic su **Crea**. La nuova pagina del voucher viene visualizzata nel riquadro di destra.

1. Apri la nuova pagina del voucher con un doppio clic, quindi fai clic su **Modifica** e configura le informazioni come richiesto.
1. Fare clic su **OK** per salvare.

1. Ora puoi attivare il voucher, in modo che gli acquirenti possano utilizzarlo nei loro carrelli sull’istanza Publish.

### Rimozione dei voucher {#removing-vouchers}

#### Rimozione dei voucher - Interfaccia classica {#removing-vouchers-classic-ui}

Per rendere un voucher non disponibile ai clienti, puoi effettuare le seguenti operazioni:

* Disattiva il voucher: rimane disponibile nell’ambiente di authoring per poterlo riattivare in un secondo momento.
* Eliminalo completamente.

Entrambe le azioni possono essere eseguite dalla console **Siti Web**.

### Modifica dei voucher {#modifying-vouchers}

#### Modifica dei voucher - Interfaccia classica {#modifying-vouchers-classic-ui}

Per modificare le proprietà di un voucher o di una promozione, fare doppio clic su di esso nella console **Siti Web** e fare clic su **Modifica**. Dopo averlo salvato, devi attivarlo in modo che le modifiche vengano inviate alle istanze di pubblicazione.

### Aggiunta di voucher a un carrello {#adding-vouchers-to-a-cart}

Per consentire agli utenti di aggiungere voucher ai carrelli, puoi utilizzare il componente predefinito **Voucher** (categoria Commerce). Aggiungilo alla stessa pagina in cui viene visualizzato il carrello (ma questo non è obbligatorio). Il componente voucher è semplicemente un modulo in cui l’utente può immettere un codice voucher; è il componente carrello che mostra effettivamente l’elenco dei voucher applicati e il relativo sconto.

Nel sito demo (Geometrixx Outdoors - inglese) puoi vedere il modulo del voucher nella pagina del carrello, sotto il carrello effettivo.

## Ordini {#orders}

>[!NOTE]
>
>È opportuno ricordare che l’AEM preconfigurato non prevede azioni necessarie per le funzionalità standard relative agli ordini, come la restituzione delle merci, l’aggiornamento dello stato degli ordini, l’evasione, la generazione dei documenti di trasporto. Si tratta principalmente di un’anteprima tecnologica.
>
>L’Order Management generico nell’AEM è stato mantenuto come standard; i campi disponibili nella procedura guidata dipendono dallo scaffold:
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

1. Utilizzando la console **Ordini**, passa alla posizione desiderata.
1. Utilizza l&#39;icona **Crea** per selezionare **Crea ordine**.

   ![Icona di creazione a forma di segno più](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Viene visualizzata la procedura guidata. Utilizza le schede **Base**, **Contenuto**, **Pagamento** e **Evasione** per immettere le [informazioni sul nuovo ordine](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Seleziona **Crea** per salvare le informazioni.

### Modifica delle informazioni dell&#39;ordine {#editing-order-information}

#### Modifica delle informazioni sull’ordine - Interfaccia utente ottimizzata per il tocco {#editing-order-information-touch-optimized-ui}

1. Utilizzando la console **Ordini**, passa all&#39;ordine.
1. Utilizzando:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità di selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona l&#39;icona **Visualizza dati ordine**:

   ![icona informazioni](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Vengono visualizzate le [informazioni ordine](/help/commerce/cif-classic/administering/concepts.md#order-information). Utilizza **Modifica** e **Fine** per apportare modifiche.

