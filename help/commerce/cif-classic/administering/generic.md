---
title: Amministrazione di eCommerce generici
seo-title: Amministrazione di eCommerce generici
description: La soluzione generica AEM fornisce metodi per gestire le informazioni di e-commerce contenute nell'archivio.
seo-description: La soluzione generica AEM fornisce metodi per gestire le informazioni di e-commerce contenute nell'archivio.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 812d1a43176a75ff22e3a0bc07bc658cb5070a62
workflow-type: tm+mt
source-wordcount: '3002'
ht-degree: 5%

---

# Amministrazione di eCommerce generici {#administering-generic-ecommerce}

La soluzione generica AEM fornisce metodi di gestione delle informazioni di e-commerce detenute all&#39;interno dell&#39;archivio (anziché utilizzare un motore di e-commerce esterno). Ciò include:

* [Prodotti](/help/commerce/cif-classic/administering/concepts.md#products)
* [Varianti prodotto](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [Catalogo](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [Promozioni](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [Voucher](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [Ordini](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Pagine proxy](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>L’installazione standard AEM include l’implementazione generica di eCommerce (JCR) AEM.
>
>Al momento questo è destinato a scopi dimostrativi o come base di partenza per un’implementazione personalizzata in base alle tue esigenze.

## Varianti di prodotti e prodotti {#products-and-product-variations}

>[!NOTE]
>
>Le procedure seguenti si applicano sia a Prodotti che a Varianti di Prodotto.

Prima di creare i prodotti è necessario definire una pagina di scaffolding [a1/>. ](/help/sites-authoring/scaffolding.md) Questo specifica i campi necessari per definire i prodotti e la relativa modalità di modifica.

Per ogni tipo di prodotto distinto è necessaria una pagina di scaffolding. La pagina di scaffolding appropriata è associata ai prodotti tramite:

* path
* il prodotto può fare riferimento alla pagina di scaffolding

>[!NOTE]
>
>Il negozio Geometrixx-Outdoors ha un singolo tipo di prodotto (e quindi un unico scaffolding):
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Il tipo di prodotto Geometrixx-Outdoors è attivo su:
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>È possibile creare una nuova definizione di prodotto in qualsiasi punto senza alcuna configurazione aggiuntiva.

### Importazione di prodotti {#importing-products}

#### Importazione di prodotti - Interfaccia touch {#importing-products-touch-optimized-ui}

1. Passa alla console **Prodotti** tramite **Commerce**.
1. Utilizzando la console **Prodotti** accedi alla posizione desiderata.
1. Utilizza l&#39;icona **Importa prodotti** per aprire la procedura guidata.

   ![chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Specifica:

   * **Importazione**

      L&#39;importazione per il [provider commerciale specifico](/help/commerce/cif-classic/administering/concepts.md#commerce-providers), per impostazione predefinita `Geometrixx`.

   * **Origine**

      Il file da importare; puoi utilizzare il browser per selezionare un file.

   * **Importazione incrementale**

      Indica se si tratta di un’importazione incrementale (anziché completa).
   >[!NOTE]
   >
   >L’importazione incrementale (del campione geometrixx-outdoor importer) opera a livello di prodotto.
   >
   >È possibile definire un importatore personalizzato in modo da funzionare come necessario.

1. Seleziona **Avanti** per importare i prodotti, verrà visualizzato un registro delle azioni eseguite.

   >[!NOTE]
   >
   >I prodotti verranno importati nella posizione corrente o in relazione a essa.

   >[!NOTE]
   >
   >L&#39;utilizzo ripetuto di **Next** e **Back** consente di importare ripetutamente le definizioni dei prodotti. Tuttavia, poiché hanno gli stessi SKU, le informazioni esistenti nell’archivio verranno semplicemente sovrascritte.

1. Seleziona **Fine** per chiudere la procedura guidata.

#### Importazione di prodotti - Interfaccia classica {#importing-products-classic-ui}

1. Utilizzando la console **Strumenti**, apri la cartella **Commerce** .
1. Fai doppio clic per aprire l&#39; **Importazione prodotti**:

   ![chlimage_1-22](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Specifica:

   * **Nome store**

      I prodotti verranno importati in:

      `/etc/commerce/products/<*store name*>/`

   * **Provider commerce**

      Importazione per il tuo [fornitore commerciale](/help/commerce/cif-classic/administering/concepts.md#commerce-providers); per impostazione predefinita, Geometrixx.

   * **File di origine**

      Posizione nell’archivio del file da importare.

   * **Importazione incrementale**

      Indica se si tratta di un’importazione incrementale (anziché completa).

1. Fare clic su **Importa prodotti**.

### Creazione di informazioni sul prodotto {#creating-product-information}

>[!NOTE]
>
>La gestione standard del prodotto è fondamentale, perché il set di prodotti Geometrixx-Outdoors è stato mantenuto di base. La complessità si basa sul prodotto [scaffolding](/help/sites-authoring/scaffolding.md), quindi con il tuo scaffolding prodotto è possibile ottenere un editing più sofisticato.

#### Creazione di informazioni sul prodotto - Interfaccia touch {#creating-product-information-touch-optimized-ui}

1. Utilizzando la console **Prodotti** (tramite **Commerce**), accedi alla posizione desiderata.
1. Utilizza l&#39;icona **Crea** per selezionare uno dei due (a seconda della struttura e della posizione):

   * **Crea prodotto**
   * **Crea variante di prodotto**

   ![chlimage_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Verrà aperta la procedura guidata. Utilizza le **Schede di base** e **Schede di prodotto** per inserire gli [attributi di prodotto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) per il nuovo prodotto o variante di prodotto.

   >[!NOTE]
   >
   >**** Titolo e  **** SKU sono il minimo necessario per creare un prodotto o una variante.

1. Selezionare **Crea** per salvare le informazioni.

>[!NOTE]
>
>Molti prodotti sono offerti in una gamma di colori e/o dimensioni. Le informazioni sul prodotto di base e le relative varianti di prodotto possono essere gestite dalla console **Products** .
>
>I prodotti e le loro varianti sono memorizzati come struttura ad albero, le informazioni sui prodotti sono nella parte superiore, con le varianti sottostanti (questa struttura viene applicata dall’interfaccia utente).

### Modifica delle informazioni sul prodotto {#editing-product-information}

>[!NOTE]
>
>Le immagini del prodotto in geometrixx-outdoors sono servite da:
>
>`/etc/commerce/products/...`
>
>Questo significa che, per impostazione predefinita, sono bloccati dal [dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html), quindi configura come necessario.

#### Modifica delle informazioni di prodotto - Interfaccia touch {#editing-product-information-touch-optimized-ui}

1. Tramite la console **Prodotti** (tramite **Commerce**) puoi accedere alle informazioni sul prodotto.
1. \nEffettuate una delle seguenti operazioni:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona l&#39;icona **Visualizza dati prodotto**:

   ![chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Verranno visualizzati gli [attributi del prodotto](/help/commerce/cif-classic/administering/concepts.md#product-attributes). Utilizza **Modifica** e **Fine** per apportare eventuali modifiche.

### Visualizzazione dei riferimenti al prodotto {#showing-product-references}

#### Visualizzazione dei riferimenti dei prodotti - Interfaccia touch {#showing-product-references-touch-optimized-ui}

1. Tramite la console **Prodotti** (tramite **Commerce**) puoi accedere alle informazioni sul prodotto.
1. Apri la barra laterale secondaria Riferimenti con l’icona :

   ![chlimage_1-4](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Seleziona il prodotto richiesto. La barra laterale secondaria verrà aggiornata per mostrare i tipi di riferimento disponibili:

   ![chlimage_1-88](/help/sites-administering/assets/chlimage_1-88.png)

1. Tocca o fai clic sul tipo di riferimento (ad esempio Pagine prodotto) per espandere l’elenco.
1. Seleziona un riferimento specifico per visualizzare le opzioni:

   * Passa a pagina prodotto
   * Modifica pagina prodotto

   ![chlimage_1-89](/help/sites-administering/assets/chlimage_1-89.png)

### Cerca prodotti {#search-for-products}

1. Passa alla console **Prodotti** tramite **Commerce**.
1. Apri la barra laterale secondaria Ricerca con l’icona :

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Sono disponibili diversi facet per la ricerca di prodotti. È possibile utilizzare solo uno o più facet per una ricerca. Verranno visualizzati i prodotti trovati:

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. Tocca o fai clic su un prodotto per aprirlo. Puoi anche pubblicarlo o visualizzare i dati del prodotto.

#### Estensione della ricerca {#extending-search}

È possibile modificare un facet esistente o aggiungerne di nuovi utilizzando CRXDE Lite:

1. Accedi a:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Ad esempio, puoi modificare le dimensioni che verranno visualizzate nella pagina di ricerca del prodotto. Fai clic sul nodo `sizegroup` .
1. Fai clic sul nodo `items`, quindi fai clic sul nodo `propertypredicate` .
1. È possibile modificare il `propertyValues`. Ad esempio, è possibile aggiungere XS o XXL o rimuovere una dimensione.
1. Fai clic su **Salva tutto** e passa alla pagina di ricerca dei prodotti. Verranno visualizzate le modifiche.

### Risorse multiple {#multiple-assets}

Puoi aggiungere più risorse nel componente prodotto, quindi specificare la risorsa che verrà visualizzata nella pagina del prodotto.

>[!NOTE]
>
>Tutte le operazioni relative a più risorse vengono eseguite con l’interfaccia touch.

#### Aggiunta di più risorse {#adding-multiple-assets}

1. Passa alla console **Prodotti** tramite **Commerce**.
1. Utilizzando la console **Prodotti**, accedi al prodotto richiesto.

   >[!NOTE]
   >
   >Devi essere a livello di prodotto, non a livello di variante.

1. Tocca o fai clic sull’icona **Visualizza dati prodotto** con la modalità di selezione o le azioni rapide.
1. Tocca o fai clic sull’icona Modifica .
1. Scorri fino a **Aggiungi**.

   ![chlimage_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. Tocca o fai clic su **Aggiungi**. Viene visualizzato un nuovo segnaposto risorsa.
1. Tocca o fai clic su **Cambia **per aprire una finestra di dialogo che consente di scegliere una risorsa.
1. Seleziona la risorsa da aggiungere.

   >[!NOTE]
   >
   >Le risorse selezionabili sono disponibili in [Risorse](/help/assets/assets.md).

1. Tocca o fai clic sull’icona Fine .

Nel componente del prodotto sono ora memorizzate due risorse. Puoi configurare quale verrà visualizzato nella pagina del prodotto. Questo funziona con un sistema di categorie. Innanzitutto devi aggiungere una categoria alle singole risorse:

1. Tocca o fai clic su **Visualizza dati prodotto**.
1. Digita una **Categoria risorse** sotto le risorse, ad esempio `cat1` e `cat2`.

   >[!NOTE]
   >
   >È inoltre possibile utilizzare i tag per le categorie.

1. Tocca o fai clic sull’icona Fine . Ora devi [eseguire il rollout](#rolling-out-a-catalog) le modifiche.

Ora le risorse nel componente prodotto hanno una categoria. Puoi configurare quale categoria verrà visualizzata a tre livelli diversi:

* [Pagina prodotto](#product-page)
* [Catalogo](#catalog)
* [Console Prodotti](#products-console)

>[!NOTE]
>
>Se non imposti categorie, la prima risorsa verrà visualizzata nella pagina del prodotto.

Il meccanismo per selezionare l&#39;immagine da visualizzare è il seguente:

1. Verifica se per la pagina di prodotto è impostata una categoria.
1. In caso contrario, verifica se è impostata una categoria per il Catalogo.
1. In caso contrario, verifica se è impostata una categoria per la console Prodotti.

>[!NOTE]
>
>Sia a livello di catalogo che a livello di console Prodotti, è necessario eseguire il rollout delle modifiche per applicare le modifiche e visualizzare la differenza nella pagina del prodotto.

#### Pagina prodotto {#product-page}

1. Passa alla pagina del prodotto.
1. **** Modifica il componente prodotto.
1. Digita la **Categoria immagine** scelta ( `cat1` ad esempio).
1. Tocca o fai clic su **Fine**. La pagina viene aggiornata e deve essere visualizzata la risorsa corretta.

#### Catalogo  {#catalog}

1. Passa al catalogo.
1. Tocca o fai clic su **Visualizza proprietà**.
1. Tocca o fai clic su **Modifica**.
1. Tocca o fai clic sulla scheda **Risorse** .
1. Digita la **categoria risorsa prodotto** richiesta.
1. Tocca o fai clic su **Fine**.
1. [](#rolling-out-a-catalog) Rollout delle modifiche.

#### Console Prodotti {#products-console}

1. Utilizzando la console **Prodotti**, accedi al prodotto richiesto.
1. Tocca o fai clic su **Visualizza dati prodotto**.
1. Tocca o fai clic su **Modifica**.
1. Digita una **Categoria risorsa predefinita**.
1. Tocca o fai clic su **Fine**.
1. [](#rolling-out-a-catalog) Rollout delle modifiche.

### Pubblicazione/annullamento della pubblicazione delle informazioni di prodotto {#publishing-unpublishing-product-information}

#### Pubblicazione/annullamento della pubblicazione delle informazioni di prodotto - Interfaccia touch {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>Spesso le informazioni sul prodotto vengono pubblicate attraverso le pagine che vi fanno riferimento. Ad esempio, quando pubblichi la pagina X che fa riferimento al prodotto Y, AEM chiederà se desideri pubblicare anche il prodotto Y.
>
>Per casi speciali, AEM supporta anche la pubblicazione diretta dai dati del prodotto.

1. Tramite la console **Prodotti** (tramite **Commerce**) puoi accedere alle informazioni sul prodotto.
1. \nEffettuate una delle seguenti operazioni:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona l&#39;icona **Pubblica** o **Annulla pubblicazione** a seconda delle necessità:

   ![chlimage_1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![chlimage_1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   Le informazioni sul prodotto saranno pubblicate o annullate la pubblicazione, a seconda dei casi.

### Feed di prodotto {#product-feed}

L’integrazione Search&amp;Promote consente di:

* utilizza l’API eCommerce, indipendentemente dalla struttura dell’archivio sottostante e dalla piattaforma commerce.
* sfrutta la funzione Connettore indice di Search&amp;Promote per fornire un feed di prodotto in formato XML.
* sfrutta la funzione di controllo remoto di Search&amp;Promote per eseguire richieste on-demand o pianificate del feed di prodotto
* generazione di feed per diversi account di Search&amp;Promote, configurati come configurazioni di cloud services.

Per ulteriori informazioni, consulta [Feed prodotto](/help/sites-administering/product-feed.md).

### Gestore eventi per aggiornamenti prodotto {#event-handler-for-product-updates}

È presente un gestore eventi che registra un evento quando un prodotto viene aggiunto, modificato o eliminato e quando viene aggiunta, modificata o eliminata una pagina di prodotto. Sono disponibili i seguenti eventi OSGi:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

Per gli eventi `PRODUCT_*`, il percorso punta al prodotto di base in `/etc/commerce/products`. Per gli eventi `PRODUCT_PAGE_*`, il percorso punta al nodo `cq:Page` .

Puoi visualizzarli nella console Web in eventi OSGI ( `/system/console/events`), ad esempio:

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Leggi anche [Gestione eventi in AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### Immagine con collegamenti Aggiungi al carrello {#image-with-add-to-cart-links}

Il componente Immagine con Aggiungi al carrello collegamenti consente di aggiungere rapidamente un prodotto al carrello creando un punto attivo collegato a un prodotto su un’immagine.

Facendo clic sul punto attivo si apre una finestra di dialogo che consente di scegliere la dimensione e la quantità del prodotto.

1. Passa alla pagina in cui desideri aggiungere il componente.
1. Trascina il componente nella pagina.
1. Trascina un’immagine nel componente dal [browser Risorse](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Puoi effettuare le seguenti operazioni:

   * fai clic sul componente e quindi sull’icona Modifica
   * fare doppio clic lento

1. Fai clic sull’icona a schermo intero.

   ![chlimage_1-92](/help/sites-administering/assets/chlimage_1-92.png)

1. Fai clic sull’icona Avvia mappa .

   ![chlimage_1-93](/help/sites-administering/assets/chlimage_1-93.png)

1. Fare clic su una delle icone della forma.

   ![chlimage_1-21](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Modificare e spostare la forma come necessario.
1. Fare clic sulla forma.
1. Facendo clic sull’icona Sfoglia si apre il [Selettore risorse](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >In alternativa, è possibile digitare direttamente il percorso del prodotto che deve essere a livello di prodotto, non il livello di variante.

   ![chlimage_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. Fai clic due volte sull’icona di conferma, quindi fai clic su esci a schermo intero.
1. Fai clic in un punto della pagina accanto al componente. La pagina dovrebbe essere aggiornata e dovresti vedere il seguente simbolo sull’immagine:

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Passa alla modalità [anteprima](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) .
1. Fai clic sul punto attivo + . Viene visualizzata una finestra di dialogo in cui puoi scegliere la dimensione e la quantità del prodotto immesso in **Percorso**.

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. Immettere una dimensione e una quantità.
1. Fai clic sul pulsante Aggiungi al carrello . La finestra di dialogo viene chiusa.
1. Passa al carrello. Il prodotto dovrebbe essere qui.

#### Opzioni di configurazione {#configuration-options}

Puoi configurare l’aspetto della finestra di dialogo quando fai clic sul punto attivo:

1. Fai clic sul componente e sull’icona configura .

   ![chlimage_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. Scorri verso il basso. È presente una scheda **AGGIUNGI AL CARRELLO** .

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. Fare clic su **AGGIUNGI AL CARRELLO**. Puoi utilizzare 3 opzioni di configurazione.

   ![chlimage_1-98](/help/sites-administering/assets/chlimage_1-98.png)

1. Fai clic sull’icona Fine .

## Cataloghi {#catalogs}

### Generazione di un catalogo {#generating-a-catalog}

#### Generazione di un catalogo - Interfaccia touch {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>Il catalogo farà riferimento ai dati del prodotto.

Per generare un catalogo:

1. Apri la console Sites (ad esempio [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Passa alla posizione in cui desideri creare la nuova pagina.
1. Per aprire l’elenco delle opzioni, usate l’icona **Crea**:

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. Seleziona **Crea catalogo** dall’elenco, si aprirà la procedura guidata Crea catalogo .

   ![chlimage_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. Passa alla Blueprint catalogo richiesta.
1. Tocca o fai clic sul pulsante **Seleziona** e tocca o fai clic sulla blueprint del catalogo richiesta.
1. Tocca o fai clic su **Avanti**.

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. Digita un **Titolo** e un **Nome**.
1. Tocca o fai clic sul pulsante **Crea** . Viene creato il catalogo e viene visualizzata una finestra di dialogo.

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. Tocca o fai clic sul pulsante **Fine** per tornare alla console Sites e visualizzare il catalogo.

   Tocca o fai clic sul pulsante **Apri catalogo** per aprire il catalogo (ad esempio `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Generazione di un catalogo - Interfaccia classica {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>Il catalogo farà riferimento ai [Dati prodotto](#products-and-product-variants).

1. Utilizzando la console **Siti web**, accedi alla **Blueprint catalogo**, quindi al Catalogo di base.

   Esempio:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Crea una nuova pagina utilizzando il modello **Blueprint di sezione** .

   Esempio, `Swimwear`.

1. Apri la nuova pagina `Swimwear`, quindi fai clic su **Modifica blueprint** per aprire la finestra di dialogo **Proprietà**, in cui puoi impostare la selezione **Prodotti** .

   Ad esempio, apri il campo **Tag/Parole chiave** per selezionare Attività, quindi Nuoto dalla sezione Geometrixx all’aperto.

1. Fare clic su **OK** per salvare le proprietà; i prodotti di esempio saranno visualizzati nella sezione **Criteri di selezione del prodotto** nella pagina blueprint.
1. Fai clic su **Rollout modifiche..**, seleziona **Rollout pagina e tutte le sottopagine**, quindi fai clic su **Avanti** e poi **Rollout**. Una volta completato correttamente il rollout, l&#39;indicatore **Stato** viene visualizzato come verde.
1. Ora puoi fare clic su **Chiudi** e controllare la nuova sezione del catalogo; ad esempio, on e under:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. Sempre dalla pagina blueprint fai clic su **Modifica blueprint** e nella finestra di dialogo **Proprietà** apri la scheda **Pagina generata** . Nel campo Elenco banner selezionare l&#39;immagine che si desidera visualizzare; ad esempio, `summer.jpg`
1. Fare clic su **OK** per salvare le proprietà; Le informazioni sul banner saranno visualizzate nella sezione **Criteri di selezione del prodotto** nella pagina blueprint.
1. Esegui il rollout di queste nuove modifiche.

### Rollout di un catalogo {#rolling-out-a-catalog}

#### Rollout di un catalogo - Interfaccia touch {#rolling-out-a-catalog-touch-optimized-ui}

Per eseguire il rollout di un catalogo:

1. Passa alla console **Cataloghi** tramite **Commerce**.
1. Passa al catalogo da eseguire.
1. \nEffettuate una delle seguenti operazioni:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona l&#39;icona **Modifiche di rollout**:

   ![rollout](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. Nella procedura guidata, imposta il rollout in base alle esigenze, quindi tocca o fai clic su **Modifiche di rollout**.
1. Viene visualizzata una finestra di dialogo. Al termine del processo, tocca/fai clic su **Fine** .

#### Rollout di un catalogo - Interfaccia classica {#rolling-out-a-catalog-classic-ui}

Per eseguire il rollout di un catalogo:

1. Passa al Catalogo di cui desideri eseguire il rollout. Esempio:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Fai clic su **Rollout modifiche..**
1. Imposta il rollout come necessario.
1. Fare clic su **Rollout**.

### Importazione blueprint {#blueprint-importer}

#### Importazione blueprint - Interfaccia touch {#blueprint-importer-touch-optimized-ui}

1. Passa alla console **Cataloghi** tramite **Commerce**.
1. Passa alla posizione in cui desideri importare la blueprint del catalogo.
1. Tocca o fai clic sull&#39;icona **Importa blueprint** .

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Nella procedura guidata, seleziona l&#39;Origine come richiesto e tocca o fai clic su **Avanti**.

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. Al termine dell’importazione, tocca/fai clic su **Fine** .

#### Importazione blueprint - Interfaccia classica {#blueprint-importer-classic-ui}

1. Utilizzando la console **Strumenti**, passa a **Commerce**.

   Esempio:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Apri la **Importazione bluprint catalogo**.
1. Imposta l’importazione come necessario.
1. Fai clic su **Importa blueprint catalogo**.

## Promozioni {#promotions}

### Creazione di una promozione {#creating-a-promotion}

#### Creazione di una promozione - Interfaccia classica {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>L&#39;esempio seguente tratta una promozione detenuta direttamente in una [campagna](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), utilizzata per i voucher.
>
>Una promozione può trovarsi anche in un’ [esperienza](/help/sites-authoring/personalization.md) all’interno di una campagna.
>
>Per ulteriori informazioni, consulta [Promozioni e voucher](#promotions-and-vouchers).

1. Apri la console **Siti web** dell’istanza di authoring.
1. Nel riquadro a sinistra seleziona la **Campagna** richiesta.
1. Fai clic su **Nuovo**, seleziona il modello **Promozione**, quindi specifica un **Titolo** (e **Nome** se necessario) per il nuovo voucher.
1. Fai clic su **Crea**. La nuova pagina della promozione verrà visualizzata nel riquadro a destra.

1. Modifica le **proprietà** effettuando una delle seguenti operazioni:

   * apri la pagina, quindi fai clic sul pulsante Modifica per aprire la finestra di dialogo Proprietà
   * selezionando la pagina nella console Siti Web e utilizzando il menu di scelta rapida (in genere il pulsante destro del mouse) per selezionare **Proprietà...** e apri la finestra di dialogo delle proprietà

   Specifica il **Tipo di promozione**, **Tipo di sconto**, **Valore di sconto** e tutti gli altri campi, a seconda delle necessità.

1. Fate clic su **OK** per salvare. 

1. Ora puoi attivare la tua promozione, in modo che gli acquirenti la vedano sull&#39;istanza di pubblicazione.

## Voucher {#vouchers}

### Creazione di un voucher {#creating-a-voucher}

#### Creazione di un voucher - Interfaccia classica {#creating-a-voucher-classic-ui}

1. Apri la console **Siti web** dell’istanza di authoring.
1. Nel riquadro a sinistra seleziona la **Campagna** richiesta.
1. Fai clic su **Nuovo**, seleziona il modello **Voucher**, quindi specifica un **Titolo** (e **Nome** se necessario) per il nuovo voucher.
1. Fai clic su **Crea**. La nuova pagina del voucher verrà visualizzata nel riquadro a destra.

1. Apri la nuova pagina del voucher con un doppio clic, quindi fai clic su **Modifica** per configurare le informazioni come necessario.
1. Fate clic su **OK** per salvare. 

1. Ora puoi attivare il tuo voucher, in modo che gli acquirenti possano usarlo nei loro carrelli sull&#39;istanza di pubblicazione.

### Rimozione dei voucher {#removing-vouchers}

#### Rimozione di voucher - Interfaccia classica {#removing-vouchers-classic-ui}

Per rendere un voucher non disponibile ai clienti, puoi:

* Disattiva il voucher : rimarrà disponibile nell’ambiente di authoring e potrai riattivarlo in un secondo momento.
* Cancellala completamente.

Entrambe le azioni possono essere eseguite dalla console **Siti web** .

### Modifica dei voucher {#modifying-vouchers}

#### Modifica dei voucher - Interfaccia classica {#modifying-vouchers-classic-ui}

Per modificare le proprietà di un voucher o di una promozione, puoi fare doppio clic su di esso nella console **Siti web** e fare clic su **Modifica**. Dopo averlo salvato, devi attivarlo in modo che le modifiche vengano inviate alle istanze di pubblicazione.

### Aggiunta di voucher a un carrello {#adding-vouchers-to-a-cart}

Per consentire agli utenti di aggiungere dei voucher ai loro carrelli, puoi utilizzare il componente **Vouchers** incorporato (categoria Commerce). È necessario aggiungerlo alla stessa pagina in cui viene visualizzato il carrello (ma non è obbligatorio). Il componente voucher è semplicemente una forma in cui l&#39;utente può inserire un codice voucher, è il componente carrello che mostra effettivamente l&#39;elenco dei voucher applicati e il loro sconto.

Nel sito demo (Geometrixx Outdoors - Inglese) potete vedere il modulo del voucher sulla pagina del carrello, sotto il carrello effettivo.

## Ordini {#orders}

>[!NOTE]
>
>Va ricordato che AEM non sono necessarie azioni per la funzionalità standard relativa agli ordini, come la restituzione di merci, l&#39;aggiornamento dello stato dell&#39;ordine, la realizzazione, la generazione di fogli di imballaggio. È progettato principalmente come anteprima tecnologica.
>
>La gestione generica degli ordini in AEM è stata mantenuta di base; i campi disponibili nella procedura guidata dipendono dalla pagina di scaffolding:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>Se si crea una pagina di scaffolding personalizzata, è possibile memorizzare ulteriori informazioni sull’ordine.

>[!NOTE]
>
>La console ordini espone le informazioni sull’ordine fornitore, che non vengono mai pubblicate.
>
>Le informazioni sull&#39;ordine del cliente vengono conservate nelle loro directory principali ed esposte dalla cronologia degli ordini per il loro account. Queste informazioni vengono pubblicate insieme al resto della loro home directory.

### Creazione di informazioni sull&#39;ordine {#creating-order-information}

#### Creazione di informazioni sull’ordine - Interfaccia touch {#creating-order-information-touch-optimized-ui}

1. Nella console **Ordini** individua la posizione desiderata.
1. Utilizza l&#39;icona **Crea** per selezionare **Crea ordine**.

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Verrà aperta la procedura guidata. Utilizza le schede **Base**, **Contenuto**, **Pagamento** e **Esecuzione** per inserire le informazioni sul nuovo ordine[.](/help/commerce/cif-classic/administering/concepts.md#order-information)

1. Selezionare **Crea** per salvare le informazioni.

### Modifica delle informazioni sull&#39;ordine {#editing-order-information}

#### Informazioni sull’ordine di modifica - Interfaccia touch {#editing-order-information-touch-optimized-ui}

1. Utilizzando la console **Ordini** , accedi all’ordine.
1. \nEffettuate una delle seguenti operazioni:

   * [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modalità selezione](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Seleziona l&#39;icona **Visualizza dati ordine**:

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Verranno visualizzate le [informazioni sull&#39;ordine](/help/commerce/cif-classic/administering/concepts.md#order-information). Utilizza **Modifica** e **Fine** per apportare eventuali modifiche.

