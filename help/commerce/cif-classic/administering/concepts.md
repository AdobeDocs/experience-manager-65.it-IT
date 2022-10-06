---
title: Concetti
description: Concetti generali di e-commerce con AEM.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '4514'
ht-degree: 1%

---

# Concetti {#concepts}

Il quadro di integrazione fornisce i meccanismi e le componenti per:

* connessione a un motore eCommerce
* estrazione dei dati in AEM
* visualizzazione di tali dati e raccolta delle risposte dell&#39;acquirente
* restituzione dei dettagli della transazione
* cerca i dati di entrambi i sistemi

Ciò significa che:

* Gli acquirenti possono registrarsi e fare acquisti senza aspettare.
* Le variazioni dei prezzi saranno visibili immediatamente dagli acquirenti.
* I prodotti possono essere aggiunti in base alle esigenze.

>[!NOTE]
>
>Il framework eCommerce può essere utilizzato con:
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [Commerce Cloud SAP](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [Commerce Cloud Salesforce](https://github.com/adobe/commerce-salesforce)
>


>[!CAUTION]
>
>La [Framework di integrazione di eCommerce](https://www.adobe.com/solutions/web-experience-management/commerce.html) è un componente aggiuntivo AEM.
>
>Il rappresentante commerciale sarà in grado di fornire tutti i dettagli, in base al motore appropriato.

>[!CAUTION]
>
>Il framework fornisce i requisiti di base per il tuo progetto.
>
>Una certa quantità di lavoro di sviluppo è sempre necessaria per adattare il framework alle tue specifiche.

>[!CAUTION]
>
>L’installazione standard AEM include l’implementazione generica di eCommerce (JCR) AEM.
>
>Al momento questo è destinato a scopi dimostrativi o come base di partenza per un’implementazione personalizzata in base alle tue esigenze.

Per ottimizzare il funzionamento, sia AEM che il motore di e-commerce si concentrano sulla propria area di competenza. Le informazioni sono trasferite tra i due in tempo reale; ad esempio:

* AEM:

   * Richiesta:

      * Informazioni sul prodotto dal motore eCommerce.
   * Fornire:

      * Visualizzazioni utente per informazioni sul prodotto, carrello acquisti e checkout.
      * Carrello acquisti e informazioni sul pagamento al motore eCommerce.
      * Ottimizzazione dei motori di ricerca (SEO).
      * Funzionalità Community.
      * Interazioni di marketing non strutturate.


* Il motore eCommerce può:

   * Fornire:

      * Informazioni di prodotto dal database.
      * Gestione delle varianti di prodotto.
      * Gestione degli ordini.
      * ERP (Enterprise Resource Planning).
      * Cerca nelle informazioni sul prodotto.
   * Processo:

      * Il carrello.
      * Il pagamento.
      * Esecuzione dell&#39;ordine.


>[!NOTE]
>
>I dettagli esatti dipenderanno dal motore eCommerce e dall’implementazione del progetto.

Per utilizzare il livello di integrazione, sono disponibili diversi componenti AEM pronti all’uso. Attualmente questi includono:

* Informazioni sul prodotto
* Carrello
* Check-out
* Account personale

Sono disponibili anche diverse opzioni di ricerca.

## Architettura {#architecture}

Il framework di integrazione fornisce l’API , una serie di componenti per illustrare funzionalità e diverse estensioni per fornire esempi di metodi di connessione:

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

Il framework consente di accedere a funzionalità quali:

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### Implementazioni {#implementations}

AEM eCommerce viene implementato con un motore eCommerce:

* Il framework di integrazione di eCommerce è stato creato per consentirti di integrare facilmente un motore di e-commerce con AEM. Il motore eCommerce appositamente progettato controlla i dati dei prodotti, i carrelli commerciali, il pagamento e l’esecuzione degli ordini, mentre AEM controlla le campagne di visualizzazione e marketing dei dati.


>[!NOTE]
>
>L’installazione standard AEM include l’implementazione generica di eCommerce (JCR) AEM.
>
>Al momento questo è destinato a scopi dimostrativi o come base di partenza per un’implementazione personalizzata in base alle tue esigenze.
>
>AEM eCommerce implementato in AEM utilizzando lo sviluppo generico basato su JCR è:
>
>* Un esempio di eCommerce autonomo e nativo AEM per illustrare l’utilizzo dell’API. Può essere utilizzato per controllare i dati dei prodotti, i carrelli commerciali e il pagamento insieme alle campagne di visualizzazione dei dati esistenti e di marketing. In questo caso il database del prodotto viene memorizzato nell&#39;archivio nativo di AEM (implementazione Adobe di [JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)).
>
>  L&#39;installazione standard AEM contiene le nozioni di base [implementazione eCommerce generica](/help/commerce/cif-classic/administering/generic.md).

### Fornitori commerciali {#commerce-providers}

Quando si importano dati da un motore di e-commerce nel sito di e-commerce AEM, viene utilizzato un provider di e-commerce per fornire i dati agli importatori. Un unico fornitore commerciale può supportare più importatori.

Un provider di servizi commerce è AEM codice personalizzato per:

* interfaccia a un motore di e-commerce back-end
* implementare un sistema commerce sopra l’archivio JCR

Per AEM sono attualmente disponibili due provider di commercio di esempio:

* uno per geometrixx-hybris
* un altro per geometrixx-generico (JCR)

Anche se in genere un progetto deve sviluppare un proprio provider di e-commerce personalizzato specifico per il proprio PIM e lo schema dei dati di prodotto.

>[!NOTE]
>
>Gli importatori geometrixx utilizzano file CSV; nei commenti sopra la loro implementazione è presente una descrizione dello schema accettato (con proprietà personalizzate consentite).

La [ProductServicesManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) mantiene [OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings))un elenco delle implementazioni  [ProductImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) e [CatalogBlueprintImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) interfacce. Sono elencati in **Fornitore importazione/commercio** campo a discesa della procedura guidata di importazione (utilizzando `commerceProvider` (come nome).

Quando un provider di importazione/commercio specifico è disponibile dal menu a discesa, tutti i dati supplementari necessari devono essere definiti (a seconda del tipo di importazione) in:

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

La cartella sotto il `importers` la cartella deve corrispondere al nome dell’importatore; ad esempio:

* `.../importproductswizard/importers/geometrixx/.content.xml`

Il formato del file di importazione di origine è definito dall’importazione. Oppure l’importatore può stabilire una connessione (ad esempio WebDAV o http) al motore di e-commerce.

## Ruoli {#roles}

Il sistema integrato gestisce i seguenti ruoli per la gestione dei dati:

* Product Information Management (PIM) Utente che gestisce:

   * Informazioni sul prodotto.
   * Tassonomia, categorizzazione, approvazione.
   * Interagisce con la gestione delle risorse digitali.
   * Prezzi - spesso questo proviene da un sistema ERP e non viene mantenuto esplicitamente nel sistema commerce.

* Autore/Marketing Manager che gestisce:

   * Contenuto marketing per tutti i canali.
   * Promozioni.
   * Voucher.
   * Campagne.

* Surfer / Shopper che:

   * Visualizza le informazioni sul prodotto.
   * Inserisce oggetti nel carrello.
   * Controlla i loro ordini.
   * Attesa evasione ordine.

Anche se la posizione effettiva può dipendere dall’implementazione; ad esempio, generico o con un motore eCommerce:

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## Prodotti {#products}

### Dati di prodotto e dati di marketing {#product-data-versus-marketing-data}

#### Categorie strutturali e di marketing {#structural-versus-marketing-categories}

Se le due categorie seguenti possono essere differenziate, questo ti consente di specificare URL chiari con una struttura significativa (alberi di `cq:Page` nodi) e quindi molto vicino alla gestione classica dei contenuti AEM):

* *Categorie strutturali

   Definizione della struttura delle categorie *che cos’è un prodotto*; ad esempio:

   `/products/mens/shoes/sneakers`

* *Marketing* categorie

   Tutte le altre categorie a *il prodotto può appartenere a*; ad esempio:

   `/special-offers/christmas/shoes`)

### Dati prodotto {#product-data}

Per rappresentare e gestire il prodotto è necessario disporre di una serie di informazioni.

I dati di prodotto possono essere:

* mantenuti direttamente in AEM (generico).
* mantenuti nel motore eCommerce e resi disponibili in AEM.

   A seconda del tipo di dati, lo è [sincronizzato](#catalog-maintenance-data-synchronization) se necessario o direttamente accessibile; ad esempio, i dati altamente volatili e critici come i prezzi dei prodotti vengono recuperati dal motore di e-commerce in ogni richiesta di pagina per assicurarsi che siano sempre aggiornati.

In entrambi i casi, quando i dati del prodotto sono stati immessi o importati in AEM, possono essere visualizzati dalla **Prodotti** console. Qui le visualizzazioni a schede ed elenco di un prodotto mostrano informazioni quali:

* l&#39;immagine
* il codice SKU
* all&#39;ultima modifica

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### Varianti prodotto {#product-variants}

Per i prodotti appropriati è inoltre possibile conservare informazioni sulle varianti. Ad esempio, per gli articoli di abbigliamento i diversi colori disponibili sono considerati varianti:

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### Attributi del prodotto {#product-attributes}

I singoli attributi contenuti in ciascun prodotto possono dipendere dal motore di eCommerce utilizzato e dall’implementazione di AEM. Sono disponibili (a seconda delle necessità) quando si visualizzano le pagine dei prodotti e/o si modificano le informazioni sui prodotti e possono includere:

* **Immagine**

   Immagine del prodotto.

* **Titolo**

   Nome del prodotto.

* **Descrizione**

   Una descrizione testuale del prodotto.

* **Tag**

   Tag utilizzati per raggruppare prodotti correlati.

* **Categoria risorse predefinita**

   Una categoria predefinita per le risorse.

* **Dati ERP**

   Informazioni sulla pianificazione delle risorse aziendali (ERP).

   * **SKU**

      Informazioni sulle unità di custodia (SKU).

   * **Colore**
   * **Dimensione**
   * **Prezzo**

      Prezzo unitario del prodotto.

* **Riepilogo**

   Riepilogo delle funzioni del prodotto.

* **Funzioni**

   Dettagli più completi sulle caratteristiche del prodotto.

### Risorse del prodotto {#product-assets}

È possibile conservare una selezione di risorse per singoli prodotti. Comunemente questi includono immagini e video.

## Cataloghi {#catalogs}

Un catalogo raggruppa i dati dei prodotti per facilitare la gestione e la rappresentazione dell’acquirente. Spesso un catalogo è strutturato in base ad attributi quali lingua, area geografica, marchio, stagione, hobby, sport, tra molti altri.

### Struttura del catalogo {#catalog-structure}

#### Cataloghi in più lingue {#catalogs-in-multiple-languages}

AEM supporta il contenuto del prodotto in più lingue. Quando si richiedono i dati, il framework di integrazione recupera la lingua dalla struttura corrente (ad esempio, `en_US` per le pagine sotto `/content/geometrixx-outdoors/en_US`).

Per un archivio multilingue, è possibile importare il catalogo per ogni struttura linguistica singolarmente (o copiarlo tramite [MSM](/help/sites-administering/msm.md)).

#### Cataloghi per più marchi {#catalogs-for-multiple-brands}

Come per le lingue, le grandi aziende multinazionali possono avere bisogno di occuparsi di più marchi.

#### Cataloghi per tag {#catalogs-by-tags}

I tag possono anche essere utilizzati per raggruppare i prodotti in un catalogo. Questi possono essere utilizzati per cataloghi più dinamici, come le offerte stagionali.

### Configurazione catalogo (importazione iniziale) {#catalog-setup-initial-import}

A seconda dell’implementazione, puoi importare i dati di prodotto necessari per il catalogo di base in AEM da:

* un file CSV (per l&#39;implementazione generica)
* il motore eCommerce

### Manutenzione del catalogo (sincronizzazione dati) {#catalog-maintenance-data-synchronization}

Ulteriori modifiche ai dati sui prodotti saranno inevitabili:

* per l&#39;implementazione generica, questi possono essere gestiti con il [editor di prodotti](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* quando si utilizza un [Motore eCommerce le modifiche devono essere sincronizzate](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### Sincronizzazione dei dati con un motore di e-commerce (in corso) {#data-synchronization-with-an-ecommerce-engine-ongoing}

Dopo l’importazione iniziale, le modifiche ai dati del prodotto sono inevitabili.

Quando si utilizza un motore di e-commerce, i dati del prodotto vengono mantenuti e devono essere disponibili in AEM. Questi dati di prodotto devono essere sincronizzati quando vengono effettuati gli aggiornamenti.

Questo può dipendere dal tipo di dati:

* A [la sincronizzazione periodica viene utilizzata insieme a un feed di dati delle modifiche](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

   Inoltre, puoi selezionare aggiornamenti specifici per un aggiornamento rapido.

* I dati altamente volatili, come le informazioni sul prezzo, vengono recuperati dal motore di e-commerce per ogni richiesta di pagina, per garantire che siano sempre aggiornati.

### Cataloghi - Prestazioni e scalabilità {#catalogs-performance-and-scaling}

L’importazione di un catalogo di grandi dimensioni con un numero elevato di prodotti (solitamente più di 100.000) da un motore di eCommerce (PIM) può influenzare il sistema a causa del numero elevato di nodi. Può anche rallentare l’istanza di authoring se i prodotti hanno risorse associate (ad esempio, immagini di prodotto). Ciò è dovuto al fatto che la post-elaborazione di queste risorse richiede un uso intensivo di CPU e memoria.

Ci sono diverse strategie che puoi scegliere di aggirare questi problemi:

* [Bucket](#bucketing) - per soddisfare il gran numero di nodi
* [Scaricare la post-elaborazione delle risorse in un’istanza dedicata](#offload-asset-post-processing-to-a-dedicated-instance)
* [Importa solo dati di prodotto](#only-import-product-data)
* [Importazione di rallentamenti e salvataggi batch](#import-throttling-and-batch-saves)
* [Test delle prestazioni](#performance-testing)
* [Prestazioni - Varie](#performance-miscellaneous)

#### Bucket {#bucketing}

Se un nodo JCR ha molti nodi figlio diretti (ad esempio 1000 e più), sono necessari bucket (cartelle fantasma) per garantire che le prestazioni non siano influenzate. Questi vengono generati in base a un algoritmo al momento dell’importazione.

Questi bucket si presentano come cartelle fantasma introdotte nella struttura del catalogo, ma possono essere configurate in modo che non siano visibili negli URL pubblici.

#### Scaricare la post-elaborazione delle risorse in un’istanza dedicata {#offload-asset-post-processing-to-a-dedicated-instance}

Questo scenario comporta l’impostazione di due istanze di authoring:

1. Istanza dell&#39;autore principale

   Importa i dati di prodotto da PIM, su cui è disabilitata la post-elaborazione per i percorsi delle risorse.

1. istanza di authoring DAM dedicata

   Importa e post-elabora le risorse di prodotto dal PIM, quindi le replica nuovamente nell&#39;istanza dell&#39;autore principale per l&#39;uso.

![Diagramma dell&#39;architettura](/help/sites-administering/assets/chlimage_1-8.png)

#### Importa solo dati di prodotto {#only-import-product-data}

Nei casi in cui i prodotti non contengono risorse (immagini) da importare, puoi importare i dati del prodotto senza essere interessati dalla post-elaborazione delle risorse.

![Diagramma dell&#39;architettura](/help/sites-administering/assets/chlimage_1-9.png)

#### Test delle prestazioni {#performance-testing}

I test delle prestazioni devono essere presi in considerazione nelle implementazioni AEM eCommerce:

* Ambiente di authoring:

   L’attività in background (ad esempio, l’importazione) può verificarsi contemporaneamente alla normale attività dell’utente (ad esempio la modifica delle pagine) e anche se le prestazioni front-end sono in genere considerate con una priorità più elevata, le prestazioni sbagliate riscontrate dagli autori online possono portare a frustrazioni in grado di bloccare una decisione go-live.

* Ambiente di pubblicazione:

   La replica è un processo fondamentale per garantire che il contenuto venga pubblicato in modo rapido e affidabile. Questo può essere influenzato dal modo in cui l’autore raggruppa i contenuti da pubblicare.

* Front-end:

   La combinazione di invalidamenti front-end e cache può potenzialmente causare sorprese nelle prestazioni. Il test aiuta a evitarli.

Tieni presente che questo test delle prestazioni richiede conoscenze e analisi del tuo obiettivo:

* Volume dei contenuti

   * Assets
   * Prodotti e SKU localizzati, I18ned

* Attività utente:

   * Edizione in serie
   * Pubblicazione in blocco
   * Richieste di ricerca intense

* Processi in background

   * Importazioni
   * Aggiornamenti alla sincronizzazione (ad esempio, prezzi)

* Requisiti di manutenzione (backup, ottimizzazione Tar PM, raccolta rifiuti del datastore, ecc.)

#### Prestazioni - Varie {#performance-miscellaneous}

Per tutte le implementazioni è possibile tenere presenti i seguenti punti:

* Come prodotto, le unità di conservazione e le categorie possono essere numerose, cercare di utilizzare il minor numero possibile di nodi per modellare il contenuto.

   Maggiore è il numero di nodi, maggiore è la flessibilità del contenuto (ad es. parsys). Tuttavia, tutto è un compromesso e hai bisogno di flessibilità individuale (per impostazione predefinita) durante la manipolazione (per esempio) dei prodotti 30K?

* Evita duplicazioni quanto puoi (consulta localizzazione) oppure, in caso affermativo, pensa a quanti nodi produrrà la duplicazione.
* Per preparare l’ottimizzazione della query, prova a assegnare il tag al contenuto il più possibile.

   Esempio:

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   deve avere un tag per livello di contenuto (ad esempio paese, lingua, categoria, marchio, prodotto). Ricerca

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   e

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   sarà drasticamente più veloce della ricerca

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* Nello stack tecnico, pianifica modelli e servizi di accesso ai contenuti molto fattoriali. Questa è una best practice generale, ma è ancora più cruciale lei, come è possibile, nelle fasi di ottimizzazione, aggiungere cache dell&#39;applicazione per i dati che vengono letti molto spesso (e che non si desidera riempire la cache del bundle con).

   Ad esempio, la gestione degli attributi è molto spesso un buon candidato per la memorizzazione in cache in quanto riguarda i dati che vengono aggiornati tramite l’importazione di prodotti.
* Considera l&#39;uso di [pagine proxy](#proxy-pages).

### Pagine delle sezioni del catalogo {#catalog-section-pages}

Le sezioni del catalogo forniscono, ad esempio:

* un’introduzione (immagine e/o testo) alla categoria; può essere utilizzato anche per striscioni e teaser per promuovere offerte speciali
* collegamenti ai singoli prodotti di tale categoria
* collegamenti alle altre categorie

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### Pagine prodotto {#product-pages}

Le pagine dei prodotti forniscono informazioni complete sui singoli prodotti. Vengono anche rispecchiati gli aggiornamenti dinamici da; ad esempio, le variazioni di prezzo registrate nel motore eCommerce.

Le pagine di prodotto sono AEM pagine che utilizzano **Prodotto** componente; ad esempio, all’interno di **Prodotto Commerce** modello:

![ecommerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

Il componente Prodotto fornisce:

* Informazioni generali sul prodotto; compresi testo e immagini.
* Prezzi; in genere viene recuperato dal motore eCommerce ogni volta che la pagina viene visualizzata o aggiornata.
* informazioni sulla variante del prodotto; ad esempio, colore e dimensione.

Queste informazioni consentono all&#39;acquirente di selezionare quanto segue quando si aggiunge un articolo al carrello:

* Varianti di colore e dimensioni
* Quantità

#### Pagine di destinazione del prodotto {#product-landing-pages}

Si tratta AEM pagine che forniscono principalmente informazioni statiche; ad esempio, un’introduzione e una panoramica con collegamenti alle pagine di prodotto sottostanti.

### Componente prodotto {#product-component}

La **Prodotto** può essere aggiunto a qualsiasi pagina con una pagina padre che fornisca i metadati richiesti (ovvero i percorsi `cartPage` e `cartObject`). Nel sito dimostrativo, i Geometrixx Outdoors sono forniti da `UserInfo.jsp`.

La **Prodotto** Il componente può anche essere personalizzato in base alle proprie esigenze.

### Pagine proxy {#proxy-pages}

Le pagine proxy vengono utilizzate per semplificare la struttura dell&#39;archivio e ottimizzare lo storage per i cataloghi di grandi dimensioni.

La creazione di un catalogo utilizza dieci nodi per prodotto in quanto fornisce singoli componenti per ogni prodotto che è possibile aggiornare e personalizzare in AEM. Questo elevato numero di nodi può diventare un problema se il catalogo contiene centinaia o persino migliaia di prodotti. Per evitare problemi è possibile creare il catalogo utilizzando le pagine proxy.

Le pagine proxy utilizzano una struttura a due nodi ( `cq:Page` e `jcr:content`) che non contiene il contenuto effettivo del prodotto. Il contenuto viene generato, al momento della richiesta, facendo riferimento ai dati del prodotto e alla pagina del modello.

Tuttavia, esiste un compromesso. Non sarà possibile personalizzare le informazioni sui prodotti in AEM, verrà utilizzato un modello standard (definito per il sito).

>[!NOTE]
>
>Non si verificheranno problemi se si importa un catalogo di grandi dimensioni senza pagine proxy.
>
>Puoi convertire da una metodologia all’altra in qualsiasi momento. Puoi anche convertire una sottosezione del catalogo.

## Promozioni e voucher {#promotions-and-vouchers}

### Voucher {#vouchers}

I voucher sono un metodo provato e collaudato di offrire sconti per attirare i consumatori nel fare un acquisto e/o premiare la fedeltà del cliente.

* Alimentazione:

   * Un codice voucher (da inserire nel carrello dall&#39;acquirente).
   * Etichetta del voucher (da visualizzare dopo che l’acquirente l’ha inserita nel carrello).
   * Un percorso di promozione (che definisce l’azione applicata al voucher).

* I motori di commercio esterno possono anche fornire buoni.

In AEM:

* Un voucher è un componente basato su pagina che viene creato/modificato con la console Siti web .
* La **Voucher** Il componente fornisce:

   * un trasformatore per l&#39;amministrazione dei buoni; questo mostra tutti i voucher attualmente nel carrello.
   * Le finestre di dialogo di modifica (modulo) per l’amministrazione (aggiunta/rimozione) dei voucher.
   * Azioni necessarie per aggiungere/rimuovere voucher al carrello o dal carrello.

* I voucher non hanno la propria data/ora di attivazione e disattivazione, ma utilizzano quelle delle campagne principali.

>[!NOTE]
>
>AEM utilizza il termine **Voucher**, questo è sinonimo di termine **Coupon**.

### Promozioni {#promotions}

Le promozioni, insieme ai voucher, consentono di realizzare scenari come:

* Un&#39;azienda fornisce prezzi personalizzati per i dipendenti, che è un elenco di utenti fatto a mano.
* I clienti a lungo termine ricevono sconti su tutti gli ordini.
* Un prezzo di vendita offerto su un periodo di tempo ben definito.
* Un cliente riceve un voucher quando il suo ordine precedente supera un importo specifico.
* Un cliente che acquista *product-X* viene offerto uno sconto il *product-Y* (prodotti coppia).

Le promozioni non vengono generalmente mantenute dai responsabili delle informazioni sui prodotti, ma dai responsabili del marketing:

* Una promozione è un componente basato su pagina che viene creato/modificato con la console Siti web . &quot;
* Offerta promozionale:

   * Una priorità
   * Un percorso handler di promozione

* Puoi collegare le promozioni a una campagna per definirne la data/ora di attivazione/disattivazione.
* Puoi collegare le promozioni a un’esperienza per definirne i segmenti.
* Le promozioni non collegate a un’esperienza non si attivano da sole, ma possono ancora essere attivate da un Voucher.
* Il componente Promozione contiene:

   * moduli di rendering e finestre di dialogo per l&#39;amministrazione delle promozioni
   * sottocomponenti per il rendering e la modifica dei parametri di configurazione specifici per i gestori della promozione

AEM le promozioni sono integrate anche nel [Campaign Management](/help/sites-authoring/personalization.md):

* a [campagna](/help/sites-authoring/personalization.md) specifica i tempi di attivazione/disattivazione
* [esperienze](/help/sites-authoring/personalization.md) *entro* la campagna viene utilizzata per raggruppare le risorse (pagine teaser, promozioni, ecc.) in base al segmento di pubblico a cui corrispondono

Una promozione può essere organizzata in un’esperienza o direttamente nella campagna:

* Se una promozione viene mantenuta in un’esperienza, può essere applicata automaticamente a un segmento di pubblico.

   Ad esempio, nel sito di esempio geometrixx-outdoors, la promozione:

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   è in un’esperienza e quindi si attiva automaticamente ogni volta che il segmento ( `ordervalueover100`).

* Se una promozione non viene visualizzata all’interno di un’esperienza (solo nella campagna), non può essere applicata automaticamente a un pubblico. Tuttavia, può ancora essere licenziato se l&#39;acquirente entra un voucher nel loro carrello e quel voucher fa riferimento alla promozione.

   Ad esempio, la promozione:

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   è al di fuori di un’esperienza e quindi non si attiva mai automaticamente (ad es: in base alla segmentazione). Tuttavia, i voucher fanno riferimento a questi ultimi che si trovano in diverse esperienze all’interno della campagna dell’articolo. L&#39;inserimento di questi codici voucher nel carrello provocherà l&#39;attivazione della promozione.

>[!NOTE]
>
>[promozioni dell&#39;hybris](https://www.hybris.com/modules/promotion) e [buoni ibridi](https://www.hybris.com/en/modules/voucher) copre tutto ciò che influenza il carrello e che è correlato ai prezzi. La promozione di contenuti di marketing specifici (come banner, ecc.) non fa parte della promozione ibrida.

## Personalizzazione {#personalization}

### Registrazione clienti e account {#customer-registration-and-accounts}

Quando un acquirente si registra, i dettagli dell’account devono essere sincronizzati tra AEM e il motore eCommerce. I dati sensibili vengono conservati in modo indipendente, ma i profili sono condivisi:

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

Il meccanismo esatto può dipendere dallo scenario:

1. Gli account utente esistono in entrambi i sistemi:

   1. Non è richiesta alcuna azione.

1. L&#39;account utente esiste solo in AEM:

   1. L’utente verrà creato nel motore eCommerce con lo stesso ID account e una password casuale che verrà memorizzata in AEM.
   1. La password casuale è necessaria, in quanto AEM tenta di accedere al motore di eCommerce alla prima chiamata (ad esempio, quando viene richiesta una pagina di prodotto e il motore di eCommerce è indicato per il prezzo). Poiché questo accade dopo l&#39;accesso AEM, la password non è disponibile.

1. L’account utente esiste solo nel motore eCommerce:

   1. L&#39;account verrà creato in AEM con lo stesso ID account e la stessa password.

Quando utilizzi un motore di eCommerce, AEM memorizza solo l’ID e la password dell’account (facoltativamente un gruppo di utenti). Tutte le altre informazioni sono memorizzate nel motore eCommerce.

>[!NOTE]
>
>Quando utilizzi un motore di eCommerce, devi assicurarti che gli account creati per gli utenti che accedono a un’istanza AEM vengano replicati (ad esempio tramite flussi di lavoro) in qualsiasi altra istanza AEM che comunica con tale motore.
>
>In caso contrario, anche queste altre istanze AEM cercheranno di creare account per gli stessi utenti nel motore. Queste azioni avranno esito negativo con un `DuplicateUidException` provenienti dal motore.

### Iscrizione al cliente {#customer-sign-up}

Spesso è necessario iscriversi perché l&#39;acquirente abbia accesso al carrello. Questo richiede la registrazione (Crea account) in modo che sia possibile creare un account specifico per il cliente.

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>È supportato anche un carrello e un pagamento anonimi.

### Accesso cliente {#customer-sign-in}

Dopo l&#39;iscrizione l&#39;acquirente può accedere con il proprio account in modo che le loro azioni possano essere monitorate e i loro ordini eseguiti.

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### Single Sign-On {#single-sign-on}

È disponibile l’accesso Single Sign-On (SSO), in modo che gli autori siano noti sia nel sistema AEM che eCommerce senza dover effettuare l’accesso due volte.

### myAccount {#myaccount}

I dati delle transazioni del motore eCommerce sono combinati con informazioni personali sull&#39;acquirente. AEM utilizza alcuni di questi dati come dati di profilo. L’azione di un modulo in AEM scrive le informazioni nel motore di eCommerce.

C&#39;è una pagina che ti consente di gestire facilmente le informazioni sul tuo account. Per accedervi, fai clic su **Il mio account** nella parte superiore di una pagina geometrixx, oppure passando a `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### Rubrica {#address-book}

Il tuo sito dovrà memorizzare una selezione di indirizzi; compresi consegna, fatturazione e indirizzi alternativi. È possibile implementarlo utilizzando moduli basati sul formato dell’indirizzo predefinito oppure utilizzando il componente Rubrica fornito da AEM.

Questo componente Rubrica consente di:

* modificare gli indirizzi nel libro
* selezionare un indirizzo dal registro per l&#39;indirizzo di spedizione
* selezionare un indirizzo dal registro per l&#39;indirizzo di fatturazione

È possibile scegliere quale indirizzo si desidera impostare come predefinito.

Il componente Rubrica è raggiungibile dal **Il mio account** facendo clic su **Rubrica** o passando a `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

Puoi fare clic su **Aggiungi nuovo indirizzo..** per aggiungere un nuovo indirizzo nella rubrica. Apre un modulo che è possibile compilare e quindi fai clic su **Aggiungi indirizzo**.

>[!NOTE]
>
>È possibile inserire più indirizzi nella Rubrica.

La Rubrica viene utilizzata per l&#39;estrazione del carrello:

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

Gli indirizzi vengono mantenuti di seguito `user_home/profile/addresses`.
Per esempio, per Alison Parker, sarebbe sotto /home/users/geometrixx/aparker@geometrixx.info/profile/addresses

Puoi scegliere l’indirizzo che desideri come impostazione predefinita. Queste informazioni vengono mantenute nel profilo dell’acquirente anziché con l’indirizzo. Proprietà profilo `address.default` viene impostato con il percorso dell&#39;indirizzo selezionato per il valore.

### Prezzi specifici per il cliente {#customer-specific-pricing}

Il motore eCommerce utilizza il contesto (essenzialmente le informazioni dell’acquirente) per determinare il prezzo che tiene, quindi fornire le informazioni corrette a AEM.

## Carrello e ordini {#shopping-cart-and-orders}

Quando si effettua lo shopping, l&#39;acquirente sfoglia le pagine dei prodotti e seleziona gli articoli da posizionare nel carrello. Quando procedono al pagamento, è possibile inserire un ordine.

### Acquirenti anonimi {#anonymous-shoppers}

Un cliente anonimo può:

* Visualizza prodotti
* Aggiungi prodotti al carrello
* Esegui il pagamento per inserire l&#39;ordine

>[!NOTE]
>
>A seconda della configurazione delle informazioni sull’indirizzo dell’istanza o della registrazione del cliente, potrebbe essere necessario prima del pagamento.

### Acquirenti registrati {#registered-shoppers}

Un cliente registrato può:

* Accedi al loro account
* Visualizza prodotti
* Aggiungi prodotti al carrello
* Esegui il pagamento per inserire l&#39;ordine
* Visualizzare e tenere traccia degli ordini precedenti

### Panoramica dei contenuti del carrello acquisti {#shopping-cart-content-overview}

Il carrello offre:

* panoramica degli elementi selezionati
* collegamenti alle pagine dei prodotti per gli elementi selezionati
* la capacità di:

   * aggiorna il numero/la quantità dei singoli articoli
   * rimuovere singoli elementi

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

Il carrello viene salvato in base al motore utilizzato:

* AEM generico memorizza il carrello in un cookie.
* Alcuni motori di e-commerce possono memorizzare il carrello in una sessione.

In entrambi i casi, gli elementi rimangono nel carrello (e possono essere ripristinati) attraverso l&#39;accesso/disconnessione (ma solo sulla stessa macchina/browser). Esempio:

* naviga come `anonymous` e aggiungere prodotti al carrello
* accedi come `Allison Parker` - il suo carrello è vuoto
* aggiungi prodotti al carrello
* disconnettiti - il carrello mostrerà i prodotti per `anonymous`

* accedi di nuovo come `Allison Parker` - i suoi prodotti sono stati ripristinati

>[!NOTE]
>
>Un carrello anonimo può essere ripristinato solo sulla stessa macchina/browser.

>[!NOTE]
>
>Non è consigliabile testare il ripristino del contenuto del carrello con il `admin` , in quanto ciò può entrare in conflitto con `admin` conto del motore eCommerce (ad esempio hybris).

>[!NOTE]
>
>hybris può essere configurato per rimuovere i carrelli in sospeso dopo un periodo di tempo definito.

Prima del pagamento, le variazioni di prezzo vengono riportate (in entrambi i sistemi) nel momento in cui si verificano.

### Informazioni ordine {#order-information}

A seconda delle informazioni di implementazione relative a un ordine nel motore eCommerce o AEM, queste informazioni vengono rese da AEM.

Vengono memorizzate diverse informazioni, tra cui:

* **ID ordine**

   Numero di riferimento per l&#39;ordine.

* **Inserito**

   Data in cui è stato effettuato l’ordine.

* **Stato**

   lo stato dell&#39;ordine; ad esempio, Spedito.

* **Valuta**

   La valuta dell&#39;ordine.

* **Elementi contenuto**

   Elenco degli elementi ordinati.

* **Subtotale**

   Costo totale degli articoli ordinati.

* **Imposte**

   Importo delle eventuali imposte dovute sull&#39;ordine.

* **Spedizione**

   Costi di spedizione.

* **Totale**

   il valore totale dell&#39;ordine; oggetti ordinati, tasse e spedizione.

* **Indirizzo di fatturazione**

   Indirizzo a cui deve essere inviata la fattura.

* **Token di pagamento**

   Metodo di pagamento.

* **Stato dei pagamenti**

   Stato del pagamento.

* **Indirizzo di spedizione**

   L&#39;indirizzo al quale le merci devono essere spedite.

* **Metodo di spedizione**

   Il metodo di spedizione; ad esempio terra, mare o aria.

* **Numero di tracciamento**

   Qualsiasi numero di registrazione utilizzato dalla società di spedizione.

* **Collegamento per tracciamento**

   Collegamento utilizzato per tenere traccia dell’ordine durante la spedizione.

>[!NOTE]
>
>I campi utilizzati nella procedura guidata per la creazione dell’ordine dipendono dal fatto che per la posizione sia stato definito uno scaffolding ottimizzato per il tocco. Nell’esempio generico, questo è disponibile all’indirizzo:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

Quando l’ordine viene mantenuto all’interno AEM console Ordine, per ogni ordine viene visualizzato quanto segue:

* il numero di elementi nel carrello
* il valore totale dell&#39;ordine
* quando è stato effettuato l&#39;ordine
* lo stato

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### Tracciamento degli ordini {#order-tracking}

Dopo aver effettuato un ordine, gli acquirenti spesso ritornano a:

* Controlla lo stato del loro ordine
* Rimuovere i prodotti dall&#39;ordine
* Aggiungi prodotti all’ordine

Dopo aver ricevuto la consegna dell&#39;ordine, gli acquirenti possono anche voler visualizzare la cronologia degli ordini effettuati in un periodo di tempo.

L’evasione e il tracciamento degli ordini sono in genere gestiti dal motore eCommerce. Le informazioni possono essere visualizzate AEM utilizzando il componente Cronologia ordini , che mostra tutti i dettagli rilevanti, inclusi i voucher e le promozioni applicate. Esempio:

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## Pagamento {#checkout}

L’estrazione è implementata con moduli AEM standard. Questo consente al responsabile marketing di personalizzare l’esperienza con i contenuti di marketing.

L’eCommerce gestisce quindi il processo di pagamento con l’input dei moduli di AEM.

### Sicurezza dei pagamenti {#payment-security}

I dettagli di pagamento, comprese le informazioni sulla carta di credito, sono spesso gestiti dal motore di eCommerce. AEM inoltrare tali informazioni transazionali al motore (da dove vengono poi inoltrate a un servizio di elaborazione dei pagamenti).

È possibile ottenere la conformità PCI (Payment Card Industry).

### Conferma dell&#39;ordine {#confirmation-of-order}

L’ordine viene confermato sullo schermo e può essere monitorato con [tracciamento degli ordini](#order-tracking).

## Ricerca {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

Poiché AEM utilizza pagine standard per i prodotti, puoi utilizzare il componente di ricerca standard per creare una pagina di ricerca.

Se hai bisogno di un’implementazione più completa, puoi:

* Estendi il componente di ricerca predefinito con la funzionalità desiderata.
* Implementa il metodo di ricerca nel tuo `CommerceService` quindi utilizza il componente di ricerca e-commerce nella pagina di ricerca.

Quando utilizzi un motore di ricerca e-commerce, l’API di ricerca e-commerce può essere completamente implementata nella soluzione motore di e-commerce, in modo da poter utilizzare il componente di ricerca e-commerce fornito come standard. La ricerca sfaccettata consente di cercare JCR e/o il motore:
