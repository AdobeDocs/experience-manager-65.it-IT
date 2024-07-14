---
title: Concetti
description: Scopri i concetti generali di e-commerce con Adobe Experience Manager.
contentOwner: Guillaume Carlino
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '4439'
ht-degree: 1%

---

# Concetti{#concepts}

Il framework di integrazione fornisce i meccanismi e i componenti necessari per:

* connessione a un motore di eCommerce
* estrazione di dati in Adobe Experience Manager (AEM)
* visualizzazione dei dati e raccolta delle risposte dell&#39;acquirente
* restituzione dei dettagli della transazione
* eseguire ricerche nei dati di entrambi i sistemi

Ciò significa che:

* Gli acquirenti possono registrarsi e fare acquisti senza attendere.
* Gli acquirenti vedono subito le variazioni di prezzo.
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
>[eCommerce Integration Framework](https://business.adobe.com/products/experience-manager/sites/ecommerce-integrations.html) è un componente aggiuntivo AEM.
>
>Il vostro rappresentante commerciale è in grado di fornire tutti i dettagli, secondo il motore appropriato.

>[!CAUTION]
>
>Il framework fornisce i requisiti di base per il progetto.
>
>È sempre necessario un certo impegno di sviluppo per adattare il framework alle proprie specifiche.

>[!CAUTION]
>
>L’installazione standard dell’AEM include l’implementazione eCommerce generica dell’AEM (JCR).
>
>Questo è a scopo dimostrativo o come base per un’implementazione personalizzata in base alle tue esigenze.

Per ottimizzare il funzionamento, sia l’AEM che il motore di eCommerce si concentrano sulla propria area di competenza. Le informazioni vengono trasferite tra i due in tempo reale, ad esempio:

* L’AEM può:

   * Richiesta:

      * Informazioni sul prodotto dal motore di eCommerce.

   * Fornisci:

      * Visualizzazioni utente per informazioni sul prodotto, carrello e pagamento.
      * Carrello acquisti e informazioni di pagamento al motore di eCommerce.
      * Ottimizzazione dei motori di ricerca (SEO).
      * Funzionalità community.
      * Interazioni di marketing non strutturate.

* Il motore di eCommerce può:

   * Fornisci:

      * Informazioni sul prodotto dal database.
      * Gestione varianti prodotto.
      * Order Management.
      * ERP (Enterprise Resource Planning).
      * Cerca nelle informazioni sul prodotto.

   * Processo:

      * Il carrello.
      * Il pagamento.
      * Evasione dell&#39;ordine.

>[!NOTE]
>
>I dettagli esatti dipendono dal motore di eCommerce e dall’implementazione del progetto.

Per utilizzare il livello di integrazione sono disponibili diversi componenti predefiniti per l’AEM. Attualmente, questi includono:

* Informazioni sul prodotto
* Carrello
* Check-out
* Account personale

Sono inoltre disponibili varie opzioni di ricerca.

## Architettura {#architecture}

Il framework di integrazione fornisce l’API, una serie di componenti per illustrare le funzionalità e diverse estensioni per fornire esempi di metodi di connessione:

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

Il framework consente di accedere a funzionalità quali:

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### Implementazioni {#implementations}

L’eCommerce dell’AEM è implementato con un motore di eCommerce:

* Il framework di integrazione dell’eCommerce è stato creato per consentirti di integrare facilmente un motore di eCommerce con l’AEM. Il motore di eCommerce appositamente creato controlla i dati dei prodotti, i carrelli, il pagamento e l’evasione degli ordini, mentre l’AEM controlla la visualizzazione dei dati e le campagne di marketing.


>[!NOTE]
>
>L’installazione standard dell’AEM include l’implementazione eCommerce generica dell’AEM (JCR).
>
>Questo è a scopo dimostrativo o come base per un’implementazione personalizzata in base alle tue esigenze.
>
>L’eCommerce AEM implementato all’interno dell’AEM utilizzando lo sviluppo generico basato sul JCR è:
>
>* Un esempio di e-commerce indipendente e nativo per l’AEM che illustra l’utilizzo dell’API. Questa può essere utilizzata per controllare i dati di prodotto, i carrelli e il pagamento con le campagne di marketing e visualizzazione dati esistenti. In questo caso, il database dei prodotti viene archiviato nell&#39;archivio nativo dell&#39;AEM (implementazione Adobe di [JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)).
>
>  L&#39;installazione AEM standard contiene le nozioni di base dell&#39;[implementazione eCommerce generica](/help/commerce/cif-classic/administering/generic.md).

### Provider Commerce {#commerce-providers}

Quando si importano dati da un motore di e-commerce nel sito eCommerce dell’AEM, viene utilizzato un provider di e-commerce per fornire i dati agli importatori. Un unico fornitore di servizi commerce può supportare più importatori.

Un provider di servizi commerce è un codice AEM personalizzato in base a:

* interfaccia con un motore di commerce back-end
* implementare un sistema commerce sopra l’archivio JCR

Due esempi di fornitori commerciali sono attualmente disponibili per l’AEM:

* uno per geometrixx-hybris
* un altro per geometrixx-generic (JCR)

Anche se in genere un progetto deve sviluppare un proprio provider di e-commerce personalizzato, specifico per il proprio schema di dati PIM e di prodotto.

>[!NOTE]
>
>Gli importatori di Geometrixx utilizzano file CSV; esiste una descrizione dello schema accettato (con le proprietà personalizzate consentite) nei commenti sopra la loro implementazione.

[ProductServicesManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) mantiene (tramite [OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)) un elenco di implementazioni delle interfacce [ProductImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) e [CatalogBlueprintImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html). Questi sono elencati nel campo a discesa **Importer/Commerce Provider** della procedura guidata di importazione (utilizzando la proprietà `commerceProvider` come nome).

Quando uno specifico provider di importazione/commercio è disponibile dal menu a discesa, tutti i dati supplementari necessari devono essere definiti (a seconda del tipo di importatore) in:

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

La cartella nella cartella `importers` appropriata deve corrispondere al nome dell&#39;importazione, ad esempio:

* `.../importproductswizard/importers/geometrixx/.content.xml`

Il formato del file di importazione di origine è definito dall&#39;importazione. In alternativa, l’importazione può stabilire una connessione (ad esempio, WebDAV o http) al motore di e-commerce.

## Ruoli {#roles}

Il sistema integrato gestisce i seguenti ruoli per mantenere i dati:

* Gestione delle informazioni sul prodotto (PIM) Utente che gestisce:

   * Informazioni sul prodotto.
   * Tassonomia, classificazione, approvazione.
   * Interagisce direttamente con la gestione delle risorse digitali.
   * Determinazione dei prezzi: spesso questo deriva da un sistema ERP e non viene mantenuto esplicitamente nel sistema commerciale.

* Autore/Marketing Manager che gestisce:

   * Contenuti di marketing per tutti i canali.
   * Promozioni
   * Voucher.
   * Campagne.

* Acquirente che:

   * Visualizza le informazioni sul prodotto.
   * Inserisce gli articoli nel carrello.
   * Esegue il check-out degli ordini.
   * Prevista evasione ordine.

Anche se la posizione effettiva può dipendere dall’implementazione; ad esempio, generica o con un motore di eCommerce:

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## Prodotti {#products}

### Dati di prodotto e dati di marketing {#product-data-versus-marketing-data}

#### Categorie strutturali e di marketing {#structural-versus-marketing-categories}

Se le due categorie seguenti possono essere differenziate, questo consente di specificare URL chiari con una struttura significativa (alberi di `cq:Page` nodi) e quindi molto vicini alla classica gestione dei contenuti AEM:

* *Categorie strutturali

  La struttura di categorie che definisce *cos&#39;è un prodotto*; ad esempio:

  `/products/mens/shoes/sneakers`

* *Marketing* categorie

  Tutte le altre categorie a cui può appartenere un *prodotto*, ad esempio:

  `/special-offers/christmas/shoes`)

### Dati prodotto {#product-data}

Per riprodurre e gestire il prodotto, è necessario disporre di una serie di informazioni.

I dati di prodotto possono essere:

* mantenuti direttamente nell’AEM (generico).
* mantenuti nel motore di eCommerce e resi disponibili nell’AEM.

  A seconda del tipo di dati, è [sincronizzato](#catalog-maintenance-data-synchronization) in base alle esigenze o vi si accede direttamente; ad esempio, dati critici e altamente volatili come i prezzi dei prodotti vengono recuperati dal motore di e-commerce in ogni richiesta di pagina per garantire che siano sempre aggiornati.

In entrambi i casi, quando i dati del prodotto sono stati immessi/importati in AEM, possono essere visualizzati dalla console **Products**. Qui le viste a schede e a elenco di un prodotto mostrano informazioni quali:

* l&#39;immagine
* il codice SKU
* quando viene modificata per ultima

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### Varianti prodotto {#product-variants}

Per i prodotti appropriati, possono essere conservate anche informazioni sulle varianti. Ad esempio, per gli articoli di abbigliamento i diversi colori disponibili sono tenuti come varianti:

![ecommerce productvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### Attributi del prodotto {#product-attributes}

I singoli attributi mantenuti per ciascun prodotto possono dipendere dal motore di eCommerce utilizzato e dall’implementazione dell’AEM. Questi sono disponibili (a seconda dei casi) quando si visualizzano pagine di prodotto e/o si modificano informazioni sul prodotto e possono includere:

* **Immagine**

  Immagine del prodotto.

* **Titolo**

  Il nome del prodotto.

* **Descrizione**

  Una descrizione testuale del prodotto.

* **Tag**

  Tag utilizzati per raggruppare i prodotti correlati.

* **Categoria risorse predefinita**

  Categoria predefinita per le risorse.

* **Dati ERP**

  Informazioni ERP (Enterprise Resource Planning).

   * **SKU**

     Informazioni sulle SKU (Stock Keeping Unit).

   * **Colore**
   * **Dimensione**
   * **Prezzo**

     Il prezzo unitario del prodotto.

* **Riepilogo**

  Riepilogo delle funzioni del prodotto.

* **Caratteristiche**

  Dettagli più completi sulle funzioni del prodotto.

### Assets del prodotto {#product-assets}

È possibile selezionare le risorse per i singoli prodotti. Di solito includono immagini e video.

## Cataloghi {#catalogs}

Un catalogo raggruppa i dati dei prodotti per semplificare la gestione e la rappresentazione da parte dell&#39;acquirente. Spesso un catalogo è strutturato in base ad attributi come lingua, area geografica, marchio, stagione, hobby, sport, tra molti altri.

### Struttura del catalogo {#catalog-structure}

#### Cataloghi in più lingue {#catalogs-in-multiple-languages}

L’AEM supporta i contenuti dei prodotti in più lingue. Quando si richiedono i dati, Integration Framework recupera il linguaggio dalla struttura corrente (ad esempio, `en_US` per le pagine in `/content/geometrixx-outdoors/en_US`).

Per un archivio multilingue, puoi importare il catalogo per ogni struttura lingua singolarmente (oppure copiarlo con [MSM](/help/sites-administering/msm.md)).

#### Cataloghi per più marchi {#catalogs-for-multiple-brands}

Come per le lingue, le grandi multinazionali devono occuparsi di più marchi.

#### Cataloghi per tag {#catalogs-by-tags}

I tag possono essere utilizzati anche per raggruppare i prodotti in un catalogo. Possono essere utilizzati per cataloghi più dinamici, ad esempio per le offerte stagionali.

### Configurazione catalogo (importazione iniziale) {#catalog-setup-initial-import}

A seconda dell’implementazione, puoi importare in AEM i dati di prodotto necessari per il catalogo di base da:

* un file CSV (per l’implementazione generica)
* il motore di eCommerce

### Manutenzione del catalogo (sincronizzazione dati) {#catalog-maintenance-data-synchronization}

Ulteriori modifiche ai dati di prodotto sono inevitabili:

* per l&#39;implementazione generica, questi possono essere gestiti con l&#39;[editor di prodotto](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* quando si utilizza un motore di [eCommerce, le modifiche devono essere sincronizzate](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### Sincronizzazione dei dati con un motore di eCommerce (in corso) {#data-synchronization-with-an-ecommerce-engine-ongoing}

Dopo l’importazione iniziale, le modifiche ai dati del prodotto sono inevitabili.

Quando si utilizza un motore di eCommerce, i dati dei prodotti vengono conservati in tale modulo e devono essere disponibili nell’AEM. Questi dati di prodotto devono essere sincronizzati quando vengono apportati aggiornamenti.

Questo può dipendere dal tipo di dati:

* Viene utilizzata una [sincronizzazione periodica insieme a un feed di dati di modifiche](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

  Inoltre, puoi selezionare aggiornamenti specifici per un aggiornamento rapido.

* Dati ad alta volatilità, come le informazioni sui prezzi, vengono recuperati dal motore di commerce per ogni richiesta di pagina, per garantire che siano sempre aggiornati.

### Cataloghi - Prestazioni e scalabilità {#catalogs-performance-and-scaling}

L’importazione di un catalogo di grandi dimensioni con un numero elevato di prodotti (più di 100.000) da un motore di eCommerce (PIM) può influire sul sistema a causa del numero elevato di nodi. Può anche rallentare l’istanza di authoring se ai prodotti sono associate delle risorse (ad esempio, immagini di prodotto). Questo perché la post-elaborazione di queste risorse richiede un uso intensivo della CPU e della memoria.

È possibile scegliere tra diverse strategie per risolvere questi problemi:

* [Bucket](#bucketing) - per gestire un numero elevato di nodi
* [Offload della post-elaborazione delle risorse in un’istanza dedicata](#offload-asset-post-processing-to-a-dedicated-instance)
* [Importa solo dati prodotto](#only-import-product-data)
* [Importa limitazione e salvataggi batch](#import-throttling-and-batch-saves)
* [Test delle prestazioni](#performance-testing)
* [Prestazioni - Varie](#performance-miscellaneous)

#### Bucket {#bucketing}

Se un nodo JCR ha molti nodi figlio diretti (ad esempio, 1000 e più), sono necessari bucket (cartelle fantasma) per garantire che le prestazioni non vengano influenzate. Questi vengono generati in base a un algoritmo durante l’importazione.

Questi bucket assumono la forma di cartelle fantasma introdotte nella struttura del catalogo, ma possono essere configurate in modo da non risultare visibili negli URL pubblici.

#### Offload della post-elaborazione delle risorse in un’istanza dedicata {#offload-asset-post-processing-to-a-dedicated-instance}

Questo scenario comporta la configurazione di due istanze di authoring:

1. Istanza autore principale

   Importa i dati di prodotto da PIM, su cui è disabilitata la post-elaborazione per i percorsi delle risorse.

1. Istanza di authoring DAM dedicata

   Importa ed esegue la post-elaborazione delle risorse di prodotto da PIM, quindi le replica nell’istanza di authoring principale per l’utilizzo.

![Diagramma architettura](/help/sites-administering/assets/chlimage_1-8.png)

#### Importa solo dati prodotto {#only-import-product-data}

Nei casi in cui i prodotti non contengano risorse (immagini) da importare, puoi importare i dati dei prodotti senza subire l’effetto della post-elaborazione delle risorse.

![Diagramma architettura](/help/sites-administering/assets/chlimage_1-9.png)

#### Test delle prestazioni {#performance-testing}

I test delle prestazioni devono essere considerati nelle implementazioni eCommerce dell’AEM:

* Ambiente di authoring:

  L’attività in background (ad esempio, l’importazione) può verificarsi contemporaneamente alla normale attività dell’utente (ad esempio, la modifica delle pagine) e anche se alle prestazioni front-end (in generale) viene assegnata una priorità più elevata, le prestazioni errate rilevate dagli autori online possono causare frustrazioni in grado di bloccare una decisione di pubblicazione.

* Ambiente di pubblicazione:

  La replica è un processo fondamentale per garantire che il contenuto venga pubblicato in modo rapido e affidabile. Questo può essere influenzato dal modo in cui l’autore raggruppa il contenuto da pubblicare.

* Front-end:

  La combinazione di invalidamenti front-end e cache può potenzialmente portare a sorprese nelle prestazioni. I test consentono di evitarli.

Tieni presente che questo test delle prestazioni richiede la conoscenza e l’analisi del target:

* Volumi di contenuto

   * Risorse
   * Prodotti e SKU localizzati I18ned

* Attività utente:

   * Modifica in serie
   * Pubblicazione in blocco
   * Richieste di ricerca intense

* Processi in background

   * Importazioni
   * Aggiornamenti della sincronizzazione (ad esempio, determinazione prezzi)

* Requisiti di manutenzione (backup, ottimizzazione Tar PM, raccolta rifiuti del datastore e così via)

#### Prestazioni - Varie {#performance-miscellaneous}

Per tutte le implementazioni, è possibile tenere presenti i seguenti punti:

* Poiché il prodotto, le unità e le categorie di stockkeeping possono essere numerose, prova a utilizzare il minor numero di nodi possibile per modellare il contenuto.

  Maggiore è il numero di nodi disponibili, maggiore è la flessibilità del contenuto (ad esempio, parsys). Tuttavia, tutto è un compromesso e hai bisogno di flessibilità individuale (per impostazione predefinita) durante la manipolazione (ad esempio) di prodotti 30K?

* Evita la duplicazione il più possibile (consulta localizzazione) o, quando lo fai, pensa a quanti nodi porta la duplicazione.
* Prova a assegnare tag al contenuto il più possibile per preparare l’ottimizzazione della query.

  Ad esempio:

  `/content/products/france/fr/shoe/reebok/pump/46 SKU`

  deve avere un tag per livello di contenuto (ovvero paese, lingua, categoria, marchio, prodotto). Ricerca

  `//element(*,my:Sku)[@country='france' and @language='fr'`

  e

  `@category='shoe' and @brand='reebok' and @product='pump']`

  sarà drasticamente più veloce che cercare

  `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* Pianifica modelli e servizi di accesso ai contenuti con factoring all’interno dello stack tecnico. Si tratta di una best practice generale, ma è ancora più fondamentale in questo caso, in quanto è possibile, nelle fasi di ottimizzazione, aggiungere cache dell’applicazione per i dati che vengono letti spesso (e di cui non si desidera riempire la cache del bundle).

  Ad esempio, la gestione degli attributi è spesso un buon candidato per il caching in quanto riguarda i dati aggiornati tramite l’importazione di prodotti.
* Valuta l&#39;utilizzo di [pagine proxy](#proxy-pages).

### Pagine sezione catalogo {#catalog-section-pages}

Le sezioni del catalogo forniscono, ad esempio:

* un’introduzione (immagine e/o testo) alla categoria; può essere utilizzata anche per banner e teaser per promuovere offerte speciali
* collegamenti ai singoli prodotti di tale categoria
* collegamenti alle altre categorie

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### Pagine prodotto {#product-pages}

Le pagine dei prodotti forniscono informazioni complete sui singoli prodotti. Vengono riflessi anche gli aggiornamenti dinamici di; ad esempio, le modifiche di prezzo registrate sul motore di eCommerce.

Le pagine dei prodotti sono pagine AEM che utilizzano il componente **Product**; ad esempio, all&#39;interno del modello **Commerce Product**:

![ecommerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

Il componente Prodotto fornisce:

* Informazioni generali sul prodotto, inclusi testo e immagini.
* Prezzi; vengono recuperati dal motore di eCommerce ogni volta che la pagina viene visualizzata o aggiornata.
* Informazioni sulla variante del prodotto, ad esempio colore e dimensioni.

Queste informazioni consentono all&#39;acquirente di selezionare quanto segue quando si aggiunge un articolo al carrello:

* Varianti di colore e dimensione
* Quantità

#### Pagine di destinazione del prodotto {#product-landing-pages}

Si tratta di pagine AEM che forniscono principalmente informazioni statiche; ad esempio, un’introduzione e una panoramica con collegamenti alle pagine di prodotto sottostanti.

### Componente prodotto {#product-component}

Il componente **Product** può essere aggiunto a qualsiasi pagina con una pagina padre che distribuisce i metadati richiesti (ovvero i percorsi di `cartPage` e `cartObject`). Nel sito dimostrativo, Geometrixx Outdoors, viene fornito da `UserInfo.jsp`.

Il componente **Prodotto** può anche essere personalizzato in base alle tue esigenze individuali.

### Pagine proxy {#proxy-pages}

Le pagine proxy vengono utilizzate per semplificare la struttura dell’archivio e ottimizzare l’archiviazione per i cataloghi di grandi dimensioni.

La creazione di un catalogo utilizza dieci nodi per prodotto, in quanto fornisce singoli componenti per ciascun prodotto che è possibile aggiornare e personalizzare in AEM. Questo numero elevato di nodi può diventare un problema se il catalogo contiene centinaia o anche migliaia di prodotti. Per evitare problemi, puoi creare il catalogo utilizzando le pagine proxy.

Le pagine proxy utilizzano una struttura a due nodi ( `cq:Page` e `jcr:content`) che non contiene alcun contenuto effettivo del prodotto. Il contenuto viene generato, al momento della richiesta, facendo riferimento ai dati del prodotto e alla pagina del modello.

Tuttavia, c&#39;è un compromesso. Non sarà possibile personalizzare le informazioni di prodotto all’interno di AEM, viene utilizzato un modello standard (definito per il sito).

>[!NOTE]
>
>Non si verificheranno problemi se si importa un catalogo di grandi dimensioni senza pagine proxy.
>
>Puoi passare da una metodologia all’altra in qualsiasi momento. Puoi anche convertire una sottosezione del catalogo.

## Promozioni e voucher {#promotions-and-vouchers}

### Voucher {#vouchers}

I voucher sono un metodo collaudato per offrire sconti al fine di attirare gli acquirenti verso un acquisto e/o premiare la fedeltà del cliente.

* Fornitura voucher:

   * Un codice voucher (che deve essere digitato nel carrello dall’acquirente).
   * Etichetta del voucher (da mostrare dopo che l&#39;acquirente l&#39;ha inserito nel carrello).
   * Un percorso di promozione (che definisce l’azione applicata dal voucher).

* Anche i motori di commercio esterno possono fornire voucher.

Per l&#39;AEM:

* Un voucher è un componente basato su pagina che viene creato/modificato con la console Siti Web.
* Il componente **Voucher** fornisce:

   * Un renderer per l&#39;amministrazione dei voucher; questo mostra tutti i voucher attualmente nel carrello.
   * Le finestre di dialogo per modifica (modulo) per l’amministrazione (aggiunta/rimozione) dei voucher.
   * Azioni necessarie per aggiungere o rimuovere i voucher dal carrello.

* I voucher non hanno date/ore di attivazione e disattivazione, ma utilizzano quelle delle campagne principali.

>[!NOTE]
>
>L&#39;AEM utilizza il termine **Voucher**, sinonimo del termine **Coupon**.

### Promozioni {#promotions}

Le promozioni, insieme ai voucher, ti permettono di realizzare scenari come:

* Un&#39;azienda fornisce prezzi personalizzati per i dipendenti, che è un elenco di utenti creato a mano.
* I clienti a lungo termine ricevono sconti su tutti gli ordini.
* Prezzo di vendita offerto in un periodo di tempo ben definito.
* Un cliente riceve un voucher quando il suo ordine precedente supera un importo specifico.
* A un cliente che acquista *product-X* viene offerto uno sconto su *product-Y* (prodotti in coppia).

Le promozioni non vengono gestite dai responsabili dell&#39;informazione sui prodotti, ma dai responsabili del marketing:

* Una promozione è un componente basato su pagina che viene creato/modificato con la console Siti web. &quot;
* Offerta promozioni:

   * Una priorità
   * Un percorso del gestore delle promozioni

* È possibile collegare le promozioni a una campagna per definirne data/ora di attivazione/disattivazione.
* Puoi collegare le promozioni a un’esperienza per definirne i segmenti.
* Le promozioni non collegate a un’esperienza non si attivano da sole, ma possono comunque essere attivate da un voucher.
* Il componente Promozione contiene:

   * renderer e finestre di dialogo per l&#39;amministrazione della promozione
   * sottocomponenti per il rendering e la modifica dei parametri di configurazione specifici dei gestori di promozioni

In AEM le promozioni sono integrate anche in [Campaign Management](/help/sites-authoring/personalization.md):

* una [campagna](/help/sites-authoring/personalization.md) specifica i tempi di attivazione/disattivazione
* [esperienze](/help/sites-authoring/personalization.md) *entro* la campagna viene utilizzata per raggruppare le risorse (pagine teaser, promozioni e così via) in base al segmento di pubblico a cui corrispondono

Una promozione può essere effettuata in un’esperienza o direttamente nella campagna:

* Se una promozione viene mantenuta in un’esperienza, può essere applicata automaticamente a un segmento di pubblico.

  Ad esempio, nel sito di esempio geometrixx-outdoors, la promozione:

  `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

  si trova in un&#39;esperienza e quindi viene attivato automaticamente ogni volta che il segmento ( `ordervalueover100`) viene risolto.

* Se una promozione non viene visualizzata all’interno di un’esperienza (solo nella campagna), non può essere applicata automaticamente a un pubblico. Tuttavia, può comunque essere attivato se il cliente inserisce un voucher nel carrello e tale voucher fa riferimento alla promozione.

  Ad esempio, la promozione:

  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

  si trova al di fuori di un’esperienza e quindi non si attiva mai automaticamente (ovvero in base alla segmentazione). Tuttavia, è indicato dai voucher che si trovano in diverse esperienze all’interno della campagna di articoli. L&#39;inserimento di tali codici voucher nel carrello determina l&#39;attivazione della promozione.

>[!NOTE]
>
>Le [promozioni ibride](https://www.hybris.com/modules/promotion) e i [voucher ibridi](https://www.hybris.com/en/modules/voucher) coprono tutto ciò che influisce sul carrello ed è relativo ai prezzi. Contenuti di marketing specifici per la promozione (come banner e così via). non fa parte della promozione hybris.

## Personalizzazione {#personalization}

### Registrazione clienti e account {#customer-registration-and-accounts}

Quando un acquirente si registra, i dettagli dell’account devono essere sincronizzati tra l’AEM e il motore di e-Commerce. I dati sensibili vengono conservati in modo indipendente, ma i profili vengono condivisi:

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

Il meccanismo esatto può dipendere dallo scenario:

1. Gli account utente esistono in entrambi i sistemi:

   1. Non è richiesta alcuna azione.

1. L’account utente esiste solo nell’AEM:

   1. L’utente viene creato nel motore di eCommerce con lo stesso ID account e una password casuale che verranno memorizzati nell’AEM.
   1. La password casuale è necessaria, in quanto l’AEM tenta di accedere al motore di eCommerce alla prima chiamata (ad esempio, quando viene richiesta una pagina di prodotto e viene fatto riferimento al motore di eCommerce per il prezzo). Poiché ciò accade dopo l’accesso AEM, la password non è disponibile.

1. L’account utente esiste solo nel motore di eCommerce:

   1. L’account viene creato in AEM con lo stesso ID account e la stessa password.

Quando si utilizza un motore di eCommerce, AEM memorizza solo l’ID account e la password (facoltativamente un gruppo di utenti). Tutte le altre informazioni vengono memorizzate nel motore di eCommerce.

>[!NOTE]
>
>Quando utilizzi un motore di eCommerce, devi assicurarti che gli account creati per gli utenti che accedono a un’istanza AEM vengano replicati (ad esempio, tramite flussi di lavoro) in qualsiasi altra istanza AEM che comunichi con tale motore.
>
>In caso contrario, anche queste altre istanze dell’AEM tenteranno di creare account per gli stessi utenti nel motore. Queste azioni non vanno a buon fine e `DuplicateUidException` proviene dal motore.

### Registrazione cliente {#customer-sign-up}

Spesso è necessaria l’iscrizione per consentire al cliente di accedere al carrello. È necessaria la registrazione (Crea account) per creare un account specifico per il cliente.

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>Sono supportati anche un carrello e un pagamento anonimi.

### Accesso del cliente {#customer-sign-in}

Dopo la registrazione, l&#39;acquirente può accedere con il proprio account in modo da poter tenere traccia delle azioni e soddisfare gli ordini.

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### Single Sign-On {#single-sign-on}

Viene fornito il Single Sign-on (SSO), in modo che gli autori siano noti sia nell’AEM che nel sistema e-Commerce senza dover effettuare il doppio accesso.

### myAccount {#myaccount}

I dati delle transazioni provenienti dal motore di eCommerce vengono combinati con le informazioni personali relative all’acquirente. L’AEM utilizza alcuni di questi dati come dati di profilo. L’azione di un modulo nell’AEM scrive le informazioni nuovamente sul motore di eCommerce.

È disponibile una pagina che consente di gestire facilmente le informazioni sull’account. Per accedervi, fai clic su **Account personale** nella parte superiore di una pagina di Geometrixx oppure passa a `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### Rubrica {#address-book}

Il sito deve memorizzare una selezione di indirizzi, inclusi consegna, fatturazione e indirizzi alternativi. È possibile implementare questa funzionalità utilizzando moduli basati sul formato di indirizzo predefinito oppure utilizzando il componente Rubrica fornito dall&#39;AEM.

Questo componente Rubrica consente di:

* modifica indirizzi nel registro
* seleziona un indirizzo dalla rubrica per l&#39;indirizzo di spedizione
* seleziona un indirizzo dalla rubrica per l&#39;indirizzo di fatturazione

È possibile scegliere l&#39;indirizzo predefinito desiderato.

Il componente Rubrica è raggiungibile dalla pagina **Account personale** facendo clic su **Rubrica** o passando a `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

È possibile fare clic su **Aggiungi nuovo indirizzo...** per aggiungere un indirizzo nella rubrica. Verrà aperto un modulo che sarà possibile compilare e quindi fare clic su **Aggiungi indirizzo**.

>[!NOTE]
>
>È possibile immettere più indirizzi nella Rubrica.

La Rubrica viene utilizzata quando si esegue il &quot;pagamento&quot; del carrello:

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

Gli indirizzi sono persistenti sotto `user_home/profile/addresses`.
Ad esempio, per Alison Parker, si troverebbe in /home/users/geometrixx/aparker@geometrixx.info/profile/addresses

Puoi scegliere l’indirizzo predefinito; queste informazioni vengono mantenute nel profilo dell’acquirente invece che con l’indirizzo. La proprietà di profilo `address.default` è impostata con il percorso dell&#39;indirizzo selezionato per il valore.

### Prezzi specifici del cliente {#customer-specific-pricing}

Il motore di eCommerce utilizza il contesto (essenzialmente le informazioni relative all’acquirente) per determinare il prezzo che detiene, quindi fornisce le informazioni corrette all’AEM.

## Carrello e ordini {#shopping-cart-and-orders}

Durante lo shopping, l’acquirente sfoglia le pagine dei prodotti e seleziona gli articoli da inserire nel carrello. Quando procedono al pagamento, è possibile effettuare un ordine.

### Acquirenti anonimi {#anonymous-shoppers}

Un cliente anonimo può:

* Visualizza prodotti
* Aggiungi prodotti al carrello
* Esegui il pagamento per effettuare l&#39;ordine

>[!NOTE]
>
>A seconda della configurazione delle informazioni sull’indirizzo dell’istanza, o della registrazione del cliente, potrebbe essere necessario prima dell’estrazione.

### Acquirenti registrati {#registered-shoppers}

Un cliente registrato può:

* Accedi al loro account
* Visualizza prodotti
* Aggiungi prodotti al carrello
* Esegui il pagamento per effettuare l&#39;ordine
* Visualizza e tiene traccia degli ordini precedenti

### Panoramica contenuti carrello {#shopping-cart-content-overview}

Il carrello fornisce:

* panoramica degli elementi selezionati
* collegamenti alle pagine dei prodotti per gli elementi selezionati
* la capacità di:

   * aggiorna il numero/quantità dei singoli articoli
   * rimuovere singoli elementi

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

Il carrello viene salvato in base al motore utilizzato:

* Un generico AEM memorizza il carrello in un cookie.
* Alcuni motori di eCommerce possono memorizzare il carrello in una sessione.

In entrambi i casi, gli elementi rimangono nel carrello (e possono essere ripristinati) durante l’accesso o la disconnessione (ma solo sullo stesso computer/browser). Ad esempio:

* sfoglia come `anonymous` e aggiungi prodotti al carrello
* accedi come `Allison Parker` - il carrello di Allison è vuoto
* aggiungi prodotti al carrello di Allison
* esci - il carrello mostra i prodotti per `anonymous`

* accedi di nuovo come `Allison Parker` - I prodotti di Allison sono ripristinati

>[!NOTE]
>
>Un carrello anonimo può essere ripristinato solo sullo stesso computer/browser.

>[!NOTE]
>
>Non è consigliabile eseguire il test per il ripristino del contenuto del carrello con l&#39;account `admin`, in quanto ciò potrebbe entrare in conflitto con l&#39;account `admin` del motore di eCommerce (ad esempio, hybris).

>[!NOTE]
>
>hybris può essere configurato per rimuovere i carrelli in sospeso dopo un periodo di tempo definito.

Prima del pagamento, le variazioni di prezzo vengono applicate (in entrambi i sistemi) nel momento in cui si verificano.

### Informazioni ordine {#order-information}

A seconda delle informazioni di implementazione relative a un ordine che si trovano nel motore di eCommerce o nell’AEM, tali informazioni vengono visualizzate dall’AEM.

Vengono memorizzate diverse informazioni, tra cui:

* **ID ordine**

  Numero di riferimento per l&#39;ordine.

* **Inserito**

  La data in cui è stato effettuato l’ordine.

* **Stato**

  Stato dell&#39;ordine, ad esempio Spedito.

* **Valuta**

  Valuta dell&#39;ordine.

* **Elementi contenuto**

  Un elenco di elementi ordinati.

* **Subtotale**

  Il costo totale degli articoli ordinati.

* **Imposta**

  L’importo di eventuali imposte dovute sull’ordine.

* **Spedizione**

  Spese di spedizione.

* **Totale**

  Il valore totale dell&#39;ordine, gli articoli ordinati, le imposte e la spedizione.

* **Indirizzo di fatturazione**

  Indirizzo a cui inviare la fattura.

* **Token di pagamento**

  Il metodo di pagamento.

* **Stato pagamento**

  Stato del pagamento.

* **Indirizzo di spedizione**

  L’indirizzo a cui devono essere spedite le merci.

* **Metodo di spedizione**

  Il metodo di spedizione, ad esempio terra, mare o aria.

* **Numero di tracciamento**

  Qualsiasi numero di registrazione utilizzato dalla società di spedizione.

* **Collegamento di tracciamento**

  Collegamento utilizzato per tenere traccia dell&#39;ordine durante la spedizione.

>[!NOTE]
>
>I campi utilizzati nella procedura guidata Crea ordine dipendono dalla definizione di uno scaffolding ottimizzato per il tocco per la posizione. Nell’esempio generico, il codice si trova in:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

Quando l’ordine viene mantenuto all’interno di AEM, la console Ordine mostra quanto segue per ogni ordine:

* il numero di articoli nel carrello
* il valore totale dell’ordine
* quando è stato effettuato l’ordine
* lo stato

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### Tracciamento ordine {#order-tracking}

Dopo aver effettuato un ordine, gli acquirenti spesso tornano a:

* Verifica lo stato del loro ordine
* Rimuovi prodotti dall&#39;ordine
* Aggiungi prodotti all&#39;ordine

Dopo aver ricevuto la consegna dell’ordine, gli acquirenti possono anche voler visualizzare la cronologia degli ordini effettuati in un periodo di tempo.

L’evasione e il tracciamento degli ordini sono gestiti dal motore di eCommerce. Le informazioni possono essere visualizzate dall’AEM utilizzando il componente Cronologia ordini, che mostra tutti i dettagli rilevanti, inclusi i voucher e le promozioni applicati. Ad esempio:

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## Ritira {#checkout}

Il checkout è implementato con i moduli standard per l’AEM. Questo consente al responsabile marketing di personalizzare l’esperienza con i contenuti di marketing.

L’eCommerce gestisce quindi il processo di pagamento con l’input dei moduli AEM.

### Sicurezza dei pagamenti {#payment-security}

I dettagli del pagamento, comprese le informazioni sulla carta di credito, sono spesso gestiti dal motore di eCommerce. L&#39;AEM inoltra tali informazioni transazionali al motore (dal quale le inoltra poi a un servizio di elaborazione dei pagamenti).

È possibile ottenere la conformità PCI (Payment Card Industry).

### Conferma dell’ordine {#confirmation-of-order}

L&#39;ordine è confermato sullo schermo e può essere tracciato con il [tracciamento dell&#39;ordine](#order-tracking).

## Ricerca {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

Poiché l’AEM utilizza pagine standard per i prodotti, puoi utilizzare il componente di ricerca standard per creare una pagina di ricerca.

Se hai bisogno di un’implementazione più completa, puoi effettuare le seguenti operazioni:

* Estendi il componente di ricerca predefinito con la funzionalità necessaria.
* Implementare il metodo di ricerca in `CommerceService` e quindi utilizzare il componente di ricerca eCommerce nella pagina di ricerca.

Quando utilizzi un motore di eCommerce, l’API di ricerca di eCommerce può essere completamente implementata nella soluzione del motore di eCommerce, in modo da poter utilizzare il componente di ricerca di eCommerce fornito come strumento pronto all’uso. La ricerca sfaccettata consente di cercare JCR e/o il motore:
