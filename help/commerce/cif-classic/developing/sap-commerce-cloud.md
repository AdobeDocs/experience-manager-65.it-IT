---
title: Sviluppo con SAP Commerce Cloud
description: Il framework di integrazione SAP Commerce Cloud include un livello di integrazione con un'API
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2296'
ht-degree: 0%

---

# Sviluppo con SAP Commerce Cloud {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>Il framework eCommerce può essere utilizzato con qualsiasi soluzione di eCommerce. Alcune specifiche ed esempi trattati in questa sede si riferiscono alla [ibrido](https://www.sap.com/products/crm.html) soluzione.

Il framework di integrazione include un livello di integrazione con un’API. Questo consente di:

* collegare un sistema eCommerce e inserire i dati dei prodotti nell’AEM

* creare componenti AEM per le funzionalità commerce indipendenti dallo specifico motore di eCommerce

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[Documentazione API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) è disponibile anche.

Per utilizzare il livello di integrazione sono disponibili diversi componenti predefiniti per l’AEM. Attualmente sono:

* un componente display di prodotto
* un carrello
* ritiro

Per la ricerca, è disponibile un hook di integrazione che consente di utilizzare la ricerca AEM, la ricerca del sistema di e-commerce, una ricerca di terze parti o una combinazione di questi elementi.

## Selezione motore di eCommerce {#ecommerce-engine-selection}

Il framework di eCommerce può essere utilizzato con qualsiasi soluzione di eCommerce, il motore utilizzato deve essere identificabile dall’AEM:

* I motori di eCommerce sono servizi OSGi che supportano `CommerceService` Interfaccia

   * I motori possono essere distinti da un `commerceProvider` service, proprietà

* Supporto AEM `Resource.adaptTo()` per `CommerceService` e `Product`

   * Il `adaptTo` l&#39;implementazione cerca un `cq:commerceProvider` nella gerarchia della risorsa:

      * Se trovato, il valore viene utilizzato per filtrare la ricerca del servizio di e-commerce.

      * Se non viene trovato, viene utilizzato il servizio di e-commerce con il livello più alto.

   * A `cq:Commerce` mixin viene utilizzato in modo che `cq:commerceProvider` alle risorse fortemente tipizzate.

* Il `cq:commerceProvider` La proprietà viene utilizzata anche per fare riferimento alla definizione di commerce factory appropriata.

   * Ad esempio, un `cq:commerceProvider` proprietà con il valore `hybris` Correlato alla configurazione OSGi per **Day CQ Commerce Factory per Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) - dove il parametro `commerceProvider` ha anche il valore `hybris`.

   * Qui ulteriori proprietà, come **Versione catalogo** possono essere configurate (se appropriate e disponibili).

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
>Utilizzando CRXDE Liti, puoi vedere come viene gestito nel componente del prodotto per l’implementazione hybris:
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### Sviluppo per hybris 4 {#developing-for-hybris}

L’estensione hybris di eCommerce Integration Framework è stata aggiornata per supportare Hybris 5, mantenendo al contempo la compatibilità con le versioni precedenti di Hybris 4.

Le impostazioni predefinite nel codice sono ottimizzate per Hybris 5.

Per sviluppare per Hybris 4 è necessario quanto segue:

* Quando richiami Maven, aggiungi il seguente argomento della riga di comando al comando

  `-P hybris4`

  Scarica la distribuzione Hybris 4 preconfigurata e la incorpora nel bundle `cq-commerce-hybris-server`.

* Nel gestore di configurazione OSGi:

   * Disattiva il supporto di Hybris 5 per il servizio Default Response Parser.

   * Assicurati che il servizio Gestore autenticazione di base Hybris abbia una classificazione del servizio inferiore rispetto al servizio Gestore OAuth Hybris.

### Gestione delle sessioni {#session-handling}

hybris utilizza una sessione utente per memorizzare informazioni quali il carrello del cliente. L’ID sessione viene restituito dall’ibrido in una `JSESSIONID` cookie che deve essere inviato su richieste successive a hybris. Per evitare di memorizzare l’ID sessione nell’archivio, viene codificato in un altro cookie memorizzato nel browser dell’acquirente. Vengono eseguiti i seguenti passaggi:

* Alla prima richiesta, non viene impostato alcun cookie sulla richiesta dell’acquirente, pertanto viene inviata una richiesta all’istanza ibrida per creare una sessione.

* I cookie di sessione vengono estratti dalla risposta, codificati in un nuovo cookie (ad esempio, `hybris-session-rest`) e impostare la risposta all&#39;acquirente. È necessaria la codifica in un nuovo cookie, perché il cookie originale è valido solo per un determinato percorso e non verrebbe altrimenti rimandato dal browser nelle richieste successive. Le informazioni sul percorso devono essere aggiunte anche al valore del cookie.

* Nelle richieste successive, i cookie vengono decodificati dal `hybris-session-<*xxx*>` cookie e impostati sul client HTTP utilizzato per richiedere dati da hybris.

>[!NOTE]
>
>Quando la sessione originale non è più valida, viene creata una nuova sessione anonima.

#### CommerceSession {#commercesession}

* Questa sessione &quot;possiede&quot; il **carrello**

   * esegue operazioni di aggiunta/rimozione/ecc.

   * esegue i vari calcoli sul carrello;

     `commerceSession.getProductPrice(Product product)`

* È il proprietario *percorso di archiviazione* per **ordine** dati

  `CommerceSession.getUserContext()`

* Possiede anche il **pagamento** elaborazione della connessione

* Possiede anche il **adempimento** connessione

### Sincronizzazione e pubblicazione dei prodotti {#product-synchronization-and-publishing}

I dati di prodotto conservati in ibridi devono essere disponibili per l’AEM. È stato attuato il seguente meccanismo:

* Un caricamento iniziale di ID viene fornito da hybris come feed. Possono esserci aggiornamenti a questo feed.
* hybris fornirà informazioni di aggiornamento tramite un feed (che i sondaggi AEM).
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

* La configurazione del catalogo in AEM riconosce **In staging** e **Online** versioni del catalogo.

* La sincronizzazione dei prodotti tra le versioni del catalogo richiede l’attivazione o la disattivazione della pagina AEM corrispondente (a, c)

   * Aggiunta di un prodotto a un **Online** la versione del catalogo richiede l’attivazione della pagina del prodotto.

   * La rimozione di un prodotto richiede la disattivazione.

* L’attivazione di una pagina in AEM (c) richiede un controllo (b) ed è possibile solo se

   * Il prodotto si trova in un **Online** versione del catalogo per le pagine di prodotti.

   * I prodotti di riferimento sono disponibili in un **Online** versione del catalogo per altre pagine (ad esempio, pagine della campagna).

* Le pagine di prodotti attivate devono accedere ai dati di prodotto di **Online** versione (d).

* L’istanza AEM Publish richiede l’accesso a ibridi per il recupero di prodotti e dati personalizzati (d).

### Architettura {#architecture}

#### Architettura del prodotto e delle varianti {#architecture-of-product-and-variants}

Un singolo prodotto può avere più varianti; ad esempio, può variare in base al colore e/o alle dimensioni. Un prodotto deve definire quali proprietà determinano la variante; termini di Adobe: *assi delle varianti*.

Tuttavia, non tutte le proprietà sono assi di variante. Le varianti possono influenzare anche altre proprietà; ad esempio, il prezzo potrebbe dipendere dalle dimensioni. Queste proprietà non possono essere selezionate dall&#39;acquirente e pertanto non sono considerate assi di variante.

Ogni prodotto e/o variante è rappresentato da una risorsa e quindi mappa 1:1 su un nodo dell’archivio. Corollario: un prodotto specifico e/o una variante possono essere identificati in modo univoco dal loro percorso.

La risorsa prodotto/variante non contiene sempre i dati effettivi del prodotto. Potrebbe trattarsi di una rappresentazione di dati conservati su un altro sistema (ad esempio ibridi). Ad esempio, le descrizioni dei prodotti, i prezzi e così via non vengono memorizzati nell’AEM, ma recuperati in tempo reale dal motore di eCommerce.

Qualsiasi risorsa di prodotto può essere rappresentata da un `Product API`. La maggior parte delle chiamate nell&#39;API del prodotto sono specifiche per le varianti (anche se le varianti potrebbero ereditare valori condivisi da un predecessore), ma ci sono anche chiamate che elencano il set di varianti ( `getVariantAxes()`, `getVariants()`e così via).

>[!NOTE]
>
>In effetti, un asse variante è determinato da qualsiasi `Product.getVariantAxes()` restituisce:
>* hybris la definisce per l’implementazione hybris
>
>Anche se i prodotti (in generale) possono avere molti assi di variante, il componente prodotto predefinito gestisce solo due elementi:
>
>1. `size`
>
>1. più un altro
>
>Questa variante aggiuntiva viene selezionata tramite `variationAxis` proprietà del riferimento al prodotto (in genere `color` per i Geometrixx Outdoors).

#### Riferimenti prodotto e dati prodotto {#product-references-and-product-data}

In generale, i dati del prodotto si trovano in `/etc`e riferimenti ai prodotti in `/content`.

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

* **Meccanismo generale di stoccaggio**

   * I nodi di prodotto sono `nt:unstructured`.

   * Un nodo prodotto può essere:

      * Un riferimento, con i dati del prodotto memorizzati altrove:

         * I riferimenti ai prodotti contengono una `productData` , che punta ai dati del prodotto (in genere sotto `/etc/commerce/products`).

         * I dati del prodotto sono gerarchici; gli attributi del prodotto vengono ereditati dai predecessori di un nodo di dati del prodotto.

         * I riferimenti ai prodotti possono anche contenere proprietà locali, che sostituiscono quelle specificate nei dati dei loro prodotti.

      * Un prodotto stesso:

         * Senza un `productData` proprietà.

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

* Il carrello è di proprietà di `CommerceSession:`

   * Il `CommerceSession` esegue operazioni di aggiunta/rimozione/ecc.
   * Il `CommerceSession` esegue anche i vari calcoli sul carrello. &quot;

* Anche se non è direttamente correlato al carrello, il `CommerceSession` deve inoltre fornire informazioni sulla determinazione dei prezzi del catalogo (in quanto è proprietario dei prezzi)

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
   * Nel caso dell’AEM-generico, i carrelli di sono conservati nel [ClientContext](/help/sites-administering/client-context.md).

**Personalizzazione**

* Guidare sempre la personalizzazione tramite [ClientContext](/help/sites-administering/client-context.md).
* Un ClientContext `/version/` del carrello viene creato in tutti i casi:

   * I prodotti devono essere aggiunti utilizzando `CommerceSession.addCartEntry()` metodo.

* Di seguito è riportato un esempio di informazioni sul carrello nel ClientContext:

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### Architettura di Checkout {#architecture-of-checkout}

**Dati carrello e ordine**

Il `CommerceSession` possiede i tre elementi seguenti:

1. Contenuto del carrello
1. Prezzi
1. I dettagli dell’ordine

1. **Contenuto del carrello**

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

   Tuttavia, i dettagli dell’ordine sono *non* risolto dall’API:

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**Calcoli spedizione**

* I moduli d’ordine spesso devono presentare più opzioni di spedizione (e prezzi).
* I prezzi possono essere basati sugli articoli e sui dettagli dell&#39;ordine, come il peso e/o l&#39;indirizzo di consegna.
* Il `CommerceSession` dispone dell’accesso a tutte le dipendenze, in modo che possa essere trattato in modo simile al prezzo del prodotto:

   * Il `CommerceSession` possiede i prezzi di spedizione.
   * È possibile recuperare/aggiornare i dettagli di consegna utilizzando `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>Puoi implementare un selettore di spedizione, ad esempio:
>
>`yourProject/commerce/components/shippingpicker`:
>
>* Essenzialmente potrebbe essere una copia di `foundation/components/form/radio`, ma con callback al `CommerceSession` per:
>
>* Verifica della disponibilità del metodo
>* Aggiunta di informazioni sui prezzi
>* Per consentire agli acquirenti di aggiornare la pagina dell&#39;ordine in AEM (incluso il superset dei metodi di spedizione e il testo che li descrive), pur mantenendo il controllo per esporre il relativo `CommerceSession` informazioni.

**Elaborazione del pagamento**

* Il `CommerceSession` è anche proprietario della connessione di elaborazione dei pagamenti.

* Gli esecutori devono aggiungere chiamate specifiche (al servizio di elaborazione dei pagamenti prescelto) al `CommerceSession` implementazione.

**Evasione ordine**

* Il `CommerceSession` possiede anche la connessione di evasione.
* Gli esecutori dovranno aggiungere chiamate specifiche (al servizio di elaborazione dei pagamenti prescelto) al `CommerceSession` implementazione.

### Definizione di ricerca {#search-definition}

Seguendo il modello API del servizio standard, il progetto eCommerce fornisce un set di API relative alla ricerca che possono essere implementate dai singoli motori di e-commerce.

>[!NOTE]
>
>Attualmente, solo il motore ibris implementa l’API di ricerca predefinita.
>
>Tuttavia, l’API di ricerca è generica e può essere implementata singolarmente da ogni CommerceService.

Il progetto eCommerce contiene un componente di ricerca predefinito, che si trova in:

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

In questo modo si utilizza l’API di ricerca per eseguire query sul motore di e-commerce selezionato (vedi [Selezione motore di eCommerce](#ecommerce-engine-selection)):

#### API di ricerca {#search-api}

Il progetto di base fornisce diverse classi generiche/helper:

1. `CommerceQuery`

   Viene utilizzato per descrivere una query di ricerca (contiene informazioni sul testo della query, sulla pagina corrente, sulle dimensioni della pagina, sull&#39;ordinamento e sui facet selezionati). Tutti i servizi eCommerce che implementano l’API di ricerca ricevono le istanze di questa classe per eseguire la ricerca. A `CommerceQuery` può essere creata un&#39;istanza da un oggetto richiesta ( `HttpServletRequest`).

1. `FacetParamHelper`

   È una classe di utilità che fornisce un metodo statico: `toParams` - utilizzato per generare `GET` stringhe di parametri da un elenco di facet e un valore attivato. Ciò è utile sul lato dell’interfaccia utente, dove è necessario visualizzare un collegamento ipertestuale per ogni valore di ciascun facet, in modo tale che quando l’utente fa clic sul collegamento ipertestuale il rispettivo valore viene attivato (ovvero, se è stato selezionato, viene rimosso dalla query, altrimenti aggiunto). In questo modo si gestisce tutta la logica necessaria per gestire facet multipli/a valore singolo, ignorare i valori e così via.

Il punto di ingresso per l’API di ricerca è `CommerceService#search` che restituisce un `CommerceResult` oggetto. Consulta la [Documentazione API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) per ulteriori informazioni su questo argomento.

### Integrazione utente {#user-integration}

L’integrazione è assicurata tra l’AEM e vari sistemi di e-commerce. Ciò richiede una strategia per sincronizzare gli acquirenti tra i vari sistemi, in modo che il codice specifico dell&#39;AEM sia a conoscenza dell&#39;AEM e viceversa:

* Autenticazione

  Si presume che l’AEM sia *solo* front-end web e quindi esegue *tutto* autenticazione.

* Account in Hybris

  L’AEM crea un conto corrispondente (subordinato) in ibridi per ogni acquirente. Il nome utente di questo account è uguale al nome utente AEM. Una password casuale e crittografica viene generata automaticamente e memorizzata (crittografata) nell’AEM.

#### Utenti preesistenti {#pre-existing-users}

Un front-end AEM può essere posizionato davanti a un’implementazione ibrida esistente. È inoltre possibile aggiungere un motore ibrido a un impianto AEM esistente. A tal fine, i sistemi devono essere in grado di gestire agevolmente gli utenti esistenti in entrambi i sistemi:

* AEM -> ibrido

   * Quando si accede a hybris, se l’utente AEM non esiste:

      * creare un nuovo utente hybris con una password casuale dal punto di vista crittografico
      * memorizza il nome utente hybris nella directory utente dell’utente AEM

   * Consulta: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`

* ibrido -> AEM

   * Quando si accede all’AEM, se il sistema riconosce l’utente:

      * tentativo di accesso a hybris con il nome utente/pwd fornito
      * in caso di esito positivo, crea il nuovo utente in AEM con la stessa password (il sale specifico per AEM si tradurrà in hash specifico per AEM)

   * L’algoritmo precedente è implementato in un Sling `AuthenticationInfoPostProcessor`

      * Consulta: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`

### Personalizzazione del processo di importazione {#customizing-the-import-process}

Per sviluppare le funzionalità esistenti, il gestore di importazione personalizzato:

* deve implementare `ImportHandler` Interfaccia

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
  * @param parentPath    Path of parent category or base path of import in case of root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

Affinché il gestore personalizzato possa essere riconosciuto dall&#39;importazione, è necessario specificare `service.ranking`proprietà con un valore superiore a 0, ad esempio.

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
