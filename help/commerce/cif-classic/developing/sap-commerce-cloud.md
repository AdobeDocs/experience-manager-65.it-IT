---
title: Sviluppo con SAP Commerce Cloud
description: Il framework di integrazione SAP Commerce Cloud include un livello di integrazione con un'API.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2303'
ht-degree: 0%

---

# Sviluppo con SAP Commerce Cloud {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>Il framework eCommerce può essere utilizzato con qualsiasi soluzione di eCommerce. Alcune specifiche ed esempi trattati qui vedono la soluzione [hybris](https://www.sap.com/products/crm.html).

Il framework di integrazione include un livello di integrazione con un’API. Questo consente di:

* collegare un sistema eCommerce e richiamare i dati dei prodotti in Adobe Experience Manager (AEM)

* creare componenti AEM per le funzionalità commerce indipendenti dallo specifico motore di eCommerce

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>È disponibile anche la [documentazione API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation).

Per utilizzare il livello di integrazione sono disponibili diversi componenti predefiniti per l’AEM. Attualmente sono:

* un componente display di prodotto
* un carrello
* ritiro

Per la ricerca, è disponibile un hook di integrazione che consente di utilizzare la ricerca AEM, la ricerca del sistema di e-commerce, una ricerca di terze parti o una combinazione di questi elementi.

## Selezione motore di eCommerce {#ecommerce-engine-selection}

Il framework di eCommerce può essere utilizzato con qualsiasi soluzione di eCommerce, il motore utilizzato deve essere identificabile dall’AEM:

* I motori eCommerce sono servizi OSGi che supportano l&#39;interfaccia `CommerceService`

   * I motori possono essere distinti da una proprietà del servizio `commerceProvider`

* AEM supporta `Resource.adaptTo()` per `CommerceService` e `Product`

   * L&#39;implementazione `adaptTo` cerca una proprietà `cq:commerceProvider` nella gerarchia della risorsa:

      * Se trovato, il valore viene utilizzato per filtrare la ricerca del servizio di e-commerce.

      * Se non viene trovato, viene utilizzato il servizio di e-commerce con il livello più alto.

   * Viene utilizzato un mixin `cq:Commerce` in modo che `cq:commerceProvider` possa essere aggiunto a risorse fortemente tipizzate.

* La proprietà `cq:commerceProvider` viene utilizzata anche per fare riferimento alla definizione di commerce factory appropriata.

   * Ad esempio, una proprietà `cq:commerceProvider` con il valore `hybris` è correlata alla configurazione OSGi per **Day CQ Commerce Factory per Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory), dove il parametro `commerceProvider` ha anche il valore `hybris`.

   * Qui è possibile configurare ulteriori proprietà, ad esempio **Versione catalogo** (quando appropriato e disponibile).

Vedi gli esempi seguenti:

| `cq:commerceProvider = geometrixx` | in un impianto AEM standard è necessaria un’implementazione specifica. Ad esempio, l’esempio di Geometrixx, che include estensioni minime all’API generica |
|--- |--- |
| `cq:commerceProvider = hybris` | implementazione hybris |

### Esempio {#example}

```shell
/content/store
+ cq:commerceProvider = hybris
  + mens
    + polo-shirt-1
    + polo-shirt-2
    + employee
+ cq:commerceProvider = jcr
  + adobe-logo-shirt
    + cq:commerceType = product
    + price = 12.50
  + adobe-logo-shirt_S
    + cq:commerceType = variant
    + size = S
  + adobe-logo-shirt_XL
    + cq:commerceType = variant
    + size = XL
    + price = 14.50
```

>[!NOTE]
>
>Utilizzando CRXDE Lite, puoi vedere come viene gestito nel componente del prodotto per l’implementazione hybris:
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### Sviluppo per hybris 4 {#developing-for-hybris}

L’estensione hybris di eCommerce Integration Framework è stata aggiornata per supportare Hybris 5, mantenendo al contempo la compatibilità con le versioni precedenti di Hybris 4.

Le impostazioni predefinite nel codice sono ottimizzate per Hybris 5.

Per sviluppare per Hybris 4, è necessario quanto segue:

* Quando richiami Maven, aggiungi il seguente argomento della riga di comando al comando

  `-P hybris4`

  Scarica la distribuzione Hybris 4 preconfigurata e la incorpora nel bundle `cq-commerce-hybris-server`.

* Nel gestore di configurazione OSGi:

   * Disattiva il supporto di Hybris 5 per il servizio Default Response Parser.

   * Assicurati che il servizio Gestore autenticazione di base Hybris abbia una classificazione del servizio inferiore rispetto al servizio Gestore OAuth Hybris.

### Gestione delle sessioni {#session-handling}

hybris utilizza una sessione utente per memorizzare informazioni quali il carrello del cliente. L&#39;ID di sessione viene restituito da hybris in un cookie `JSESSIONID` che deve essere inviato alle richieste successive a hybris. Per evitare di memorizzare l’ID sessione nell’archivio, viene codificato in un altro cookie memorizzato nel browser dell’acquirente. Vengono eseguiti i seguenti passaggi:

* Alla prima richiesta, non viene impostato alcun cookie sulla richiesta dell’acquirente, pertanto viene inviata una richiesta all’istanza ibrida per creare una sessione.

* I cookie di sessione vengono estratti dalla risposta, codificati in un nuovo cookie (ad esempio, `hybris-session-rest`) e impostati sulla risposta all&#39;acquirente. È necessaria la codifica in un nuovo cookie, perché il cookie originale è valido solo per un determinato percorso e non verrebbe altrimenti rimandato dal browser nelle richieste successive. Le informazioni sul percorso devono essere aggiunte al valore del cookie.

* Nelle richieste successive, i cookie vengono decodificati dai cookie `hybris-session-<*xxx*>` e impostati sul client HTTP utilizzato per richiedere i dati da hybris.

>[!NOTE]
>
>Quando la sessione originale non è più valida, viene creata una nuova sessione anonima.

#### CommerceSession {#commercesession}

* Questa sessione &quot;possiede&quot; il **carrello**

   * esegue operazioni di aggiunta/rimozione/ecc.

   * esegue i vari calcoli sul carrello;

     `commerceSession.getProductPrice(Product product)`

* Possiede il *percorso di archiviazione* per i dati **order**

  `CommerceSession.getUserContext()`

* È proprietario della connessione di elaborazione **pagamento**

* È il proprietario della connessione **fulfilment**

### Sincronizzazione e pubblicazione dei prodotti {#product-synchronization-and-publishing}

I dati di prodotto conservati in ibridi devono essere disponibili per l’AEM. È stato attuato il seguente meccanismo:

* Un caricamento iniziale di ID viene fornito da hybris come feed. Possono esserci aggiornamenti a questo feed.
* hybris fornisce informazioni di aggiornamento tramite un feed (che viene consultato dall’AEM).
* Quando l’AEM utilizza i dati del prodotto, invia nuovamente le richieste all’ibrido per i dati correnti (richiesta di recupero condizionale utilizzando la data dell’ultima modifica).
* Su Hybris, è possibile specificare il contenuto dei mangimi in modo dichiarativo.
* La mappatura della struttura del feed sul modello del contenuto dell’AEM avviene nell’adattatore del feed sul lato dell’AEM.

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* L’importatore (b) viene utilizzato per la configurazione iniziale della struttura ad albero della pagina in AEM per i cataloghi.
* Le variazioni del catalogo ibrido sono indicate all&#39;AEM tramite un feed, che poi si propagano all&#39;AEM (b)

   * Prodotto aggiunto/eliminato/modificato relativo alla versione del catalogo.

   * Prodotto approvato.

* L’estensione hybris fornisce un importazione polling (&quot;schema ibrido&quot;), che può essere configurato per importare le modifiche nell’AEM a un intervallo specificato (ad esempio, ogni 24 ore in cui l’intervallo è specificato in secondi):

  ```JavaScript
      http://localhost:4502/content/geometrixx-outdoors/en_US/jcr:content.json
       {
       * "jcr:mixinTypes": ["cq:PollConfig"],
       * "enabled": true,
       * "source": "hybris:outdoors",
       * "jcr:primaryType": "cq:PageContent",
       * "interval": 86400
       }
  ```

* La configurazione del catalogo in AEM riconosce **Versioni del catalogo in staging** e **Online**.

* La sincronizzazione dei prodotti tra le versioni del catalogo richiede l’attivazione o la disattivazione della pagina AEM corrispondente (a, c)

   * L&#39;aggiunta di un prodotto a una versione del catalogo **Online** richiede l&#39;attivazione della pagina del prodotto.

   * La rimozione di un prodotto richiede la disattivazione.

* L’attivazione di una pagina in AEM (c) richiede un controllo (b) ed è possibile solo se

   * Il prodotto è in una versione del catalogo **Online** per le pagine di prodotti.

   * I prodotti a cui si fa riferimento sono disponibili in una versione del catalogo **Online** per altre pagine, ad esempio le pagine della campagna.

* Le pagine di prodotti attivate devono accedere alla versione **Online** (d) dei dati di prodotto.

* L’istanza Publish dell’AEM richiede l’accesso a hybris per il recupero di prodotti e dati personalizzati (d).

### Architettura {#architecture}

#### Architettura del prodotto e delle varianti {#architecture-of-product-and-variants}

Un singolo prodotto può avere più varianti; ad esempio, può variare in base al colore e/o alle dimensioni. Un prodotto deve definire quali proprietà guidano la variante; l&#39;Adobe definisce questi *assi di variante*.

Tuttavia, non tutte le proprietà sono assi di variante. Le varianti possono influenzare anche altre proprietà; ad esempio, il prezzo potrebbe dipendere dalle dimensioni. Queste proprietà non possono essere selezionate dall&#39;acquirente e pertanto non sono considerate assi di variante.

Ogni prodotto e/o variante è rappresentato da una risorsa e quindi mappa 1:1 su un nodo dell’archivio. Corollario: un prodotto specifico e/o una variante possono essere identificati in modo univoco dal loro percorso.

La risorsa prodotto/variante non contiene sempre i dati effettivi del prodotto. Potrebbe trattarsi di una rappresentazione di dati conservati su un altro sistema (ad esempio ibridi). Ad esempio, le descrizioni dei prodotti e i prezzi non vengono memorizzati in AEM, ma recuperati in tempo reale dal motore di eCommerce.

Qualsiasi risorsa prodotto può essere rappresentata da `Product API`. La maggior parte delle chiamate nell&#39;API del prodotto sono specifiche per la variante (anche se le varianti potrebbero ereditare valori condivisi da un predecessore), ma ci sono anche chiamate che elencano il set di varianti ( `getVariantAxes()`, `getVariants()` e così via).

>[!NOTE]
>
>In effetti, un asse variante è determinato da qualsiasi valore restituito da `Product.getVariantAxes()`:
>* hybris la definisce per l’implementazione hybris
>
>Anche se i prodotti (in generale) possono avere molti assi di variante, il componente prodotto predefinito gestisce solo due elementi:
>
>1. `size`
>
>1. più un altro
>
>Questa variante aggiuntiva viene selezionata tramite la proprietà `variationAxis` del riferimento prodotto (in genere `color` per i Geometrixx Outdoors).

#### Riferimenti prodotto e dati prodotto {#product-references-and-product-data}

In generale, i dati di prodotto si trovano in `/etc` e i riferimenti di prodotto in `/content`.

È necessaria una mappa 1:1 tra varianti di prodotto e nodi di dati del prodotto.

Anche i riferimenti di prodotto devono avere un nodo per ogni variante presentata, ma non è necessario presentare tutte le varianti. Ad esempio, se un prodotto ha varianti S, M, L, i dati del prodotto potrebbero essere:

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

Mentre un catalogo &quot;Big and Tall&quot; potrebbe avere solo:

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
```

Infine, non è necessario utilizzare i dati di prodotto. Puoi inserire tutti i dati di prodotto sotto i riferimenti nel catalogo; ma in tal caso non puoi disporre di più cataloghi senza duplicare tutti i dati di prodotto.

**API**

#### com.adobe.cq.commerce.api.Product interface {#com-adobe-cq-commerce-api-product-interface}

```java
public interface Product extends Adaptable {

    public String getPath();            // path to specific variation
    public String getPagePath();        // path to presentation page for all variations
    public String getSKU();             // unique ID of specific variation

    public String getTitle();           // shortcut to getProperty(TITLE)
    public String getDescription();     // shortcut to getProperty(DESCRIPTION)
    public String getImageUrl();        // shortcut to getProperty(IMAGE_URL)
    public String getThumbnailUrl();    // shortcut to getProperty(THUMBNAIL_URL)

    public <T> T getProperty(String name, Class<T> type);

    public Iterator<String> getVariantAxes();
    public boolean axisIsVariant(String axis);
    public Iterator<Product> getVariants(VariantFilter filter) throws CommerceException;
}
```

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * for example, when using {@link Product#getVariants(VariantFilter filter)}.
 */
public interface VariantFilter {
    public boolean includes(Product product);
}

/**
 * A {@link VariantFilter} for filtering variants by the given
 * axis and value. The following example returns a list of
 * variant products that have a value of <i>blue</i> on the
 * <i>color</i> axis.
 *
 * <p>
 * <code>product.getVariants(new AxisFilter("color", "blue"));</code>
 */
public class AxisFilter implements VariantFilter {

    private String axis;
    private String value;

    public AxisFilter(String axis, String value) {
        this.axis = axis;
        this.value = value;
    }

    /**
     * {@inheritDoc}
     */
    public boolean includes(Product product) {
        ValueMap values = product.adaptTo(ValueMap.class);

        if(values != null) {
            String v = values.get(axis, String.class);

            return v != null && v == value;
        }

        return false;
    }
}
```

* **Meccanismo di archiviazione generale**

   * Nodi prodotto: `nt:unstructured`.

   * Un nodo prodotto può essere:

      * Un riferimento, con i dati del prodotto memorizzati altrove:

         * I riferimenti al prodotto contengono una proprietà `productData` che punta ai dati del prodotto (in genere sotto `/etc/commerce/products`).

         * I dati del prodotto sono gerarchici; gli attributi del prodotto vengono ereditati dai predecessori di un nodo di dati del prodotto.

         * I riferimenti ai prodotti possono anche contenere proprietà locali, che sostituiscono quelle specificate nei dati dei loro prodotti.

      * Un prodotto stesso:

         * Senza una proprietà `productData`.

         * Un nodo di prodotto che contiene tutte le proprietà localmente (e non contiene una proprietà productData) eredita gli attributi di prodotto direttamente dai propri predecessori.

* **Struttura di prodotto AEM-generica**

   * Ogni variante deve avere un proprio nodo foglia.

   * L’interfaccia del prodotto rappresenta sia prodotti che varianti, ma il nodo dell’archivio correlato è specifico per quello che è.

   * Il nodo prodotto descrive gli attributi del prodotto e gli assi delle varianti.

#### Esempio {#example-1}

```shell
+ banyan_shirt
    - cq:commerceType = product
    - cq:productAttributes = [jcr:title, jcr:description, size, price, color]
    - cq:productVariantAxes = [color, size]
    - jcr:title = Banyan Shirt
    - jcr:description = Flowery, all-cotton shirt.
    - price = 14.00
    + banyan_shirt_s
        - cq:commerceType = variant
        - size = S
        + banyan_shirt_s_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_s_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_m
        - cq:commerceType = variant
        - size = M
        + banyan_shirt_m_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_m_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_l
        - cq:commerceType = variant
        - size = L
        + banyan_shirt_l_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_l_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_xl
        - cq:commerceType = variant
        - size = XL
        - price = 18.00
```

#### Architettura del carrello {#architecture-of-the-shopping-cart}

**Componenti**

* Il carrello appartiene a `CommerceSession:`

   * `CommerceSession` esegue operazioni di aggiunta o rimozione e così via.
   * `CommerceSession` esegue anche i vari calcoli sul carrello. &quot;

* Sebbene non sia direttamente correlato al carrello, `CommerceSession` deve anche fornire informazioni sui prezzi del catalogo (in quanto è proprietario dei prezzi)

   * I prezzi possono avere diversi modificatori:

      * Sconti sulla quantità.
      * Valute diverse.
      * IVA esente e IVA esente.

   * I modificatori sono open-end con la seguente interfaccia:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**Archiviazione**

* Archiviazione

   * Nel caso dell’ibrido, il server ibrido è il proprietario del carrello.
   * Nel caso AEM-generico, i carrelli di sono memorizzati nel [ClientContext](/help/sites-administering/client-context.md).

**Personalizzazione**

* Esegui sempre la personalizzazione tramite il [ClientContext](/help/sites-administering/client-context.md).
* Viene creato un ClientContext `/version/` del carrello in tutti i casi:

   * I prodotti devono essere aggiunti utilizzando il metodo `CommerceSession.addCartEntry()`.

* Di seguito è riportato un esempio di informazioni sul carrello nel ClientContext:

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### Architettura di Checkout {#architecture-of-checkout}

**Dati carrello e ordine**

`CommerceSession` possiede i tre elementi:

1. Contenuto del carrello
1. Prezzi
1. I dettagli dell’ordine

1. **Contenuto carrello**

   Lo schema del contenuto del carrello è fisso dall’API:

   ```java
   public void addCartEntry(Product product, int quantity);
   public void modifyCartEntry(int entryNumber, int quantity);
   public void deleteCartEntry(int entryNumber);
   ```

1. **Prezzi**

   Lo schema di determinazione dei prezzi è fissato anche dall’API:

   ```java
   public String getCartPreTaxPrice();
   public String getCartTax();
   public String getCartTotalPrice();
   public String getOrderShipping();
   public String getOrderTotalTax();
   public String getOrderTotalPrice();
   ```

1. **Dettagli ordine**

   Tuttavia, i dettagli dell&#39;ordine sono *non* corretti dall&#39;API:

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**Calcoli di spedizione**

* I moduli d’ordine spesso devono presentare più opzioni di spedizione (e prezzi).
* I prezzi possono essere basati sugli articoli e sui dettagli dell&#39;ordine, come il peso e/o l&#39;indirizzo di consegna.
* `CommerceSession` ha accesso a tutte le dipendenze, quindi può essere trattato in modo simile al prezzo del prodotto:

   * A `CommerceSession` appartengono i prezzi di spedizione.
   * È possibile recuperare/aggiornare i dettagli di consegna utilizzando `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>Puoi implementare un selettore di spedizione, ad esempio:
>
>`yourProject/commerce/components/shippingpicker`:
>
>* In sostanza potrebbe trattarsi di una copia di `foundation/components/form/radio`, ma con callback a `CommerceSession` per:
>
>* Verifica della disponibilità del metodo
>* Aggiunta di informazioni sui prezzi
>* Per consentire agli acquirenti di aggiornare la pagina dell&#39;ordine in AEM (incluso il superset dei metodi di spedizione e il testo che li descrive), pur mantenendo il controllo per esporre le informazioni `CommerceSession` rilevanti.

**Elaborazione pagamento**

* `CommerceSession` è anche proprietario della connessione di elaborazione dei pagamenti.

* Gli implementatori devono aggiungere chiamate specifiche (al servizio di elaborazione dei pagamenti scelto) all&#39;implementazione `CommerceSession`.

**Evasione ordine**

* `CommerceSession` è anche proprietario della connessione di evasione.
* Gli implementatori devono aggiungere chiamate specifiche (al servizio di elaborazione dei pagamenti scelto) all&#39;implementazione `CommerceSession`.

### Definizione di ricerca {#search-definition}

Seguendo il modello API del servizio standard, il progetto eCommerce fornisce un set di API relative alla ricerca che possono essere implementate dai singoli motori di e-commerce.

>[!NOTE]
>
>Attualmente, solo il motore ibris implementa l’API di ricerca predefinita.
>
>Tuttavia, l’API di ricerca è generica e può essere implementata singolarmente da ogni CommerceService.

Il progetto eCommerce contiene un componente di ricerca predefinito in:

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

In questo modo viene utilizzata l&#39;API di ricerca per eseguire una query sul motore di eCommerce selezionato (vedere [Selezione del motore di eCommerce](#ecommerce-engine-selection)):

#### API di ricerca {#search-api}

Il progetto di base fornisce diverse classi generiche/helper:

1. `CommerceQuery`

   Descrive una query di ricerca (contiene informazioni sul testo della query, sulla pagina corrente, sulle dimensioni della pagina, sull&#39;ordinamento e sui facet selezionati). Tutti i servizi eCommerce che implementano l’API di ricerca ricevono istanze di questa classe per eseguire la ricerca. È possibile creare un&#39;istanza di `CommerceQuery` da un oggetto richiesta ( `HttpServletRequest`).

1. `FacetParamHelper`

   Classe di utilità che fornisce un metodo statico, `toParams`, utilizzato per generare `GET` stringhe di parametri da un elenco di facet e un valore attivato. Ciò è utile sul lato dell’interfaccia utente, dove è necessario visualizzare un collegamento ipertestuale per ogni valore di ciascun facet, in modo tale che quando l’utente fa clic sul collegamento ipertestuale il rispettivo valore venga attivato. In altre parole, se è stata selezionata, viene rimossa dalla query, altrimenti viene aggiunta. In questo modo si gestisce tutta la logica necessaria per gestire facet multipli/a valore singolo, ignorare i valori e così via.

Il punto di ingresso per l&#39;API di ricerca è il metodo `CommerceService#search` che restituisce un oggetto `CommerceResult`. Per ulteriori informazioni su questo argomento, consulta la [documentazione API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation).

### Integrazione utente {#user-integration}

L’integrazione è assicurata tra l’AEM e vari sistemi di e-commerce. Ciò richiede una strategia per sincronizzare gli acquirenti tra i vari sistemi, in modo che il codice specifico dell&#39;AEM sia a conoscenza dell&#39;AEM e viceversa:

* Autenticazione

  Si presume che AEM sia il front-end Web *only* ed esegue pertanto l&#39;autenticazione *all*.

* Account in Hybris

  L’AEM crea un conto corrispondente (subordinato) in ibridi per ogni acquirente. Il nome utente di questo account è uguale al nome utente AEM. Una password casuale e crittografica viene generata automaticamente e memorizzata (crittografata) nell’AEM.

#### Utenti preesistenti {#pre-existing-users}

Un front-end AEM può essere posizionato davanti a un’implementazione ibrida esistente. È inoltre possibile aggiungere un motore ibrido a un impianto AEM esistente. A tal fine, i sistemi devono essere in grado di gestire agevolmente gli utenti esistenti in entrambi i sistemi:

* AEM > ibrido

   * Quando si accede a hybris, se l’utente AEM non esiste:

      * creare un utente hybris con una password casuale dal punto di vista crittografico
      * memorizza il nome utente hybris nella directory utente dell’utente AEM

   * Vedere: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`

* hybris > AEM

   * Quando si accede all’AEM, se il sistema riconosce l’utente:

      * tentativo di accesso a hybris con il nome utente/pwd fornito
      * in caso di esito positivo, crea l’utente in AEM con la stessa password (il sale specifico per AEM restituisce l’hash specifico per AEM)

   * L&#39;algoritmo precedente è implementato in un Sling `AuthenticationInfoPostProcessor`

      * Vedere: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`

### Personalizzazione del processo di importazione {#customizing-the-import-process}

Per sviluppare le funzionalità esistenti, il gestore di importazione personalizzato:

* deve implementare l&#39;interfaccia `ImportHandler`

* può estendere `DefaultImportHandler`.

```java
/**
 * Services implementing the <code>ImportHandler</code> interface are
 * called by the {@link HybrisImporter} to create actual commerce entities
 * such as products.
 */
public interface ImportHandler {

  /**
  * Not used.
  */
  public void createTaxonomie(ImporterContext ctx);

  /**
  * Creates a catalog with the given name.
  * @param ctx   The importer context
  * @param name  The catalog's name
  * @return Path of created catalog
  */
  public String createCatalog(ImporterContext ctx, String name) throws Exception;

  /**
  * Creates a product from the given values.
  * @param ctx                The importer context
  * @param values             The product's properties
  * @param parentCategoryPath The containing category's path
  * @return Path of created product
  */
  public String createProduct(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;

  /**
  * Creates a variant product from the given values.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The base product's path
  * @return Path of created product
  */
  public String createVariantProduct(ImporterContext ctx, ValueMap values, String baseProductPath) throws Exception;

  /**
  * Creates an asset for a product. This is usually a product
  * image.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The product's path
  * @return Path of created asset
  */
  public String createAsset(ImporterContext ctx, ValueMap values, String productPath) throws Exception;

  /**
  * Creates a category from the given values.
  * @param ctx           The importer context
  * @param values        The category's properties
  * @param parentPath    Path of parent category or base path of import if there is a root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

Affinché il gestore personalizzato possa essere riconosciuto dall&#39;importazione, è necessario, ad esempio, specificare la proprietà `service.ranking` con un valore maggiore di 0.

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
