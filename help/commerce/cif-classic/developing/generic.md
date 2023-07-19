---
title: Sviluppo (generico)
seo-title: Developing (generic)
description: Il framework di integrazione include un livello di integrazione con un’API che consente di creare componenti AEM per le funzionalità di eCommerce
seo-description: The integration framework includes an integration layer with an API, allowing you to build AEM components for eCommerce capabilities
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---

# Sviluppo (generico){#developing-generic}

>[!NOTE]
>
>[Documentazione API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) è disponibile anche.

Il framework di integrazione include un livello di integrazione con un’API. Questo consente di creare componenti AEM per le funzionalità di eCommerce (indipendentemente dal motore di eCommerce specifico). Consente inoltre di utilizzare il database interno CRX o di collegare un sistema di e-commerce e richiamare i dati dei prodotti nell’AEM.

Per utilizzare il livello di integrazione è disponibile una serie di componenti AEM pronti all’uso. Attualmente sono:

* Un componente display di prodotto
* Un carrello
* Promozioni e voucher
* Blueprint di cataloghi e sezioni
* Check-out
* Ricerca

Per la ricerca è disponibile un hook di integrazione che consente di utilizzare la ricerca AEM, una ricerca di terze parti o una combinazione delle due.

## Selezione motore di eCommerce {#ecommerce-engine-selection}

Il framework di eCommerce può essere utilizzato con qualsiasi soluzione di eCommerce, il motore utilizzato deve essere identificato dall’AEM - anche quando si utilizza il motore generico dell’AEM:

* I motori di eCommerce sono servizi OSGi che supportano `CommerceService` Interfaccia

   * I motori possono essere distinti da un `commerceProvider` service, proprietà

* Supporto AEM `Resource.adaptTo()` per `CommerceService` e `Product`

   * Il `adaptTo` l&#39;implementazione cerca un `cq:commerceProvider` nella gerarchia della risorsa:

      * Se trovato, il valore viene utilizzato per filtrare la ricerca del servizio di e-commerce.
      * Se non viene trovato, viene utilizzato il servizio di e-commerce con il livello più alto.

   * A `cq:Commerce` mixin viene utilizzato in modo che `cq:commerceProvider` alle risorse fortemente tipizzate.

* Il `cq:commerceProvider` La proprietà viene utilizzata anche per fare riferimento alla definizione di commerce factory appropriata.

   * Ad esempio, un `cq:commerceProvider` con il valore geometrixx sarà correlata alla configurazione OSGi per **Day CQ Commerce Factory per Geometrixx-Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`) - dove il parametro `commerceProvider` ha anche il valore `geometrixx`.
   * Qui è possibile configurare altre proprietà (quando appropriato e disponibile).

In un’installazione standard AEM è necessaria un’implementazione specifica, ad esempio:

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | esempio di geometrixx; questo include estensioni minime all’API generica |

### Esempio {#example}

```shell
/etc/commerce/products/geometrixx-outdoors
+ cq:commerceProvider = geometrixx
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
>Utilizzando CRXDE Lite puoi vedere come viene gestito nel componente del prodotto per l’implementazione generica dell’AEM:
>
>`/apps/geometrixx-outdoors/components/product`

### Gestione delle sessioni {#session-handling}

Sessione per memorizzare le informazioni relative al carrello del cliente.

Il **CommerceSession**:

* È il proprietario **carrello**

   * esegue operazioni di aggiunta/rimozione/ecc.
   * esegue i vari calcoli sul carrello;

     `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Possiede la persistenza del **ordine** dati:

  `CommerceSession.getUserContext()`

* È possibile recuperare/aggiornare i dettagli di consegna utilizzando `updateOrder(Map<String, Object> delta)`
* Possiede anche il **pagamento** elaborazione della connessione
* Possiede anche il **adempimento** connessione

### Architettura {#architecture}

#### Architettura del prodotto e delle varianti {#architecture-of-product-and-variants}

Un singolo prodotto può avere più varianti; ad esempio, può variare in base al colore e/o alle dimensioni. Un prodotto deve definire quali proprietà determinano la variazione; questi vengono definiti *assi delle varianti*.

Tuttavia, non tutte le proprietà sono assi di variante. Le varianti possono influenzare anche altre proprietà; ad esempio, il prezzo potrebbe dipendere dalle dimensioni. Queste proprietà non possono essere selezionate dall&#39;acquirente e pertanto non sono considerate assi di variante.

Ogni prodotto e/o variante è rappresentato da una risorsa e quindi mappa 1:1 su un nodo dell’archivio. Corollario: un prodotto specifico e/o una variante possono essere identificati in modo univoco dal loro percorso.

Qualsiasi risorsa di prodotto può essere rappresentata da un `Product API`. La maggior parte delle chiamate nell&#39;API del prodotto sono specifiche per le varianti (anche se le varianti potrebbero ereditare valori condivisi da un predecessore), ma ci sono anche chiamate che elencano il set di varianti ( `getVariantAxes()`, `getVariants()`, ecc.).

>[!NOTE]
>
>In effetti, un asse variante è determinato da qualsiasi `Product.getVariantAxes()` restituisce:
>
>* per l’implementazione generica, l’AEM lo legge da una proprietà nei dati del prodotto ( `cq:productVariantAxes`)
>
>Anche se i prodotti (in generale) possono avere molti assi di variante, il componente prodotto predefinito gestisce solo due elementi:
>
>1. `size`
>1. più un altro
>
>   Questa variante aggiuntiva viene selezionata tramite `variationAxis` proprietà del riferimento al prodotto (in genere `color` per i Geometrixx Outdoors).

#### Riferimenti prodotto e dati PIM {#product-references-and-pim-data}

In generale:

* I dati PIM si trovano in `/etc`

* Riferimenti prodotto in `/content`.

È necessaria una mappa 1:1 tra varianti di prodotto e nodi di dati del prodotto.

Anche i riferimenti di prodotto devono avere un nodo per ogni variante presentata, ma non è necessario presentare tutte le varianti. Ad esempio, se un prodotto ha varianti S, M, L, i dati del prodotto potrebbero essere:

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

Mentre un catalogo &quot;Big and Tall&quot; potrebbe avere solo:

```shell
content
  big-and-tall
    shirt
      shirt-l
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

   * I nodi prodotto non sono:non strutturati.
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

   * Il `CommerceSession` esegue operazioni di aggiunta, rimozione e così via.
   * Il `CommerceSession` esegue anche i vari calcoli sul carrello.
   * Il `CommerceSession` applica anche voucher e promozioni che sono stati attivati sul carrello.

* Anche se non è direttamente correlato al carrello, il `CommerceSession` deve inoltre fornire informazioni sulla determinazione dei prezzi del catalogo (in quanto è proprietario dei prezzi)

   * I prezzi possono avere diversi modificatori:

      * Sconti sulla quantità.
      * Valute diverse.
      * IVA esente e IVA esente.

   * I modificatori sono completamente aperti con la seguente interfaccia:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**Archiviazione**

* Archiviazione

   * Nel caso dell’AEM-generico, i carrelli di sono conservati nel [ClientContext](/help/sites-administering/client-context.md)

**Personalizzazione**

* La personalizzazione deve sempre essere guidata attraverso [ClientContext](/help/sites-administering/client-context.md).
* Un ClientContext `/version/` del carrello viene creato in tutti i casi:

   * I prodotti devono essere aggiunti utilizzando `CommerceSession.addCartEntry()` metodo.

* Di seguito è riportato un esempio di informazioni sul carrello nel ClientContext:

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### Architettura di Checkout {#architecture-of-checkout}

**Dati carrello e ordine**

Il `CommerceSession` possiede i tre elementi seguenti:

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
   * Utilizzare `updateOrder(Map<String, Object> delta)` per recuperare/aggiornare i dettagli di consegna.

### Definizione di ricerca {#search-definition}

Seguendo il modello API del servizio standard, il progetto eCommerce fornisce un set di API relative alla ricerca che possono essere implementate dai singoli motori di e-commerce.

>[!NOTE]
>
>Attualmente, solo il motore ibris implementa l’API di ricerca predefinita.
>
>Tuttavia, l’API di ricerca è generica e può essere implementata singolarmente da ogni CommerceService.
>
>Pertanto, anche se l’implementazione generica fornita non implementa questa API, puoi estenderla e aggiungere la funzionalità di ricerca.

Il progetto eCommerce contiene un componente di ricerca predefinito, che si trova in:

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

In questo modo si utilizza l’API di ricerca per eseguire query sul motore di e-commerce selezionato (vedi [Selezione motore di eCommerce](#ecommerce-engine-selection)):

#### API di ricerca {#search-api}

Il progetto di base fornisce diverse classi generiche/helper:

1. `CommerceQuery`

   Viene utilizzato per descrivere una query di ricerca (contiene informazioni sul testo della query, sulla pagina corrente, sulle dimensioni della pagina, sull&#39;ordinamento e sui facet selezionati). Tutti i servizi eCommerce che implementano l’API di ricerca riceveranno istanze di questa classe per eseguire la ricerca. A `CommerceQuery` può essere creata un&#39;istanza da un oggetto richiesta ( `HttpServletRequest`).

1. `FacetParamHelper`

   È una classe di utilità che fornisce un metodo statico: `toParams` - utilizzato per generare `GET` stringhe di parametri da un elenco di facet e un valore attivato. Questa funzione è utile nell’interfaccia utente, dove è necessario visualizzare un collegamento ipertestuale per ogni valore di ciascun facet, in modo tale che quando l’utente fa clic sul collegamento ipertestuale il rispettivo valore viene attivato (ovvero se è stato selezionato, viene rimosso dalla query, altrimenti aggiunto). In questo modo si prende cura di tutta la logica necessaria per gestire facet multipli/a valore singolo, sostituire valori, ecc.

Il punto di ingresso per l’API di ricerca è `CommerceService#search` che restituisce un `CommerceResult` oggetto. Per ulteriori informazioni su questo argomento, consulta la documentazione dell’API.

### Sviluppo di promozioni e voucher {#developing-promotions-and-vouchers}

* Voucher:

   * Un voucher è un componente basato su pagina che viene creato/modificato con la console Siti web e memorizzato in:

     `/content/campaigns`

   * Fornitura voucher:

      * Un codice voucher (che deve essere digitato nel carrello dall’acquirente).
      * Etichetta del voucher (da mostrare dopo che l&#39;acquirente l&#39;ha inserito nel carrello).
      * Un percorso di promozione (che definisce l&#39;azione applicata dal voucher).

   * I voucher non hanno date/ore di attivazione e disattivazione, ma utilizzano quelle delle campagne principali.
   * I motori di commercio esterno possono anche fornire buoni; questi richiedono un minimo di:

      * Un codice voucher
      * Un `isValid()` metodo

   * Il **Voucher** componente ( `/libs/commerce/components/voucher`) fornisce:

      * Un renderer per l&#39;amministrazione dei voucher; questo mostra tutti i voucher attualmente nel carrello.
      * Le finestre di dialogo per modifica (modulo) per l’amministrazione (aggiunta/rimozione) dei voucher.
      * Azioni necessarie per aggiungere o rimuovere i voucher dal carrello.

* Promozioni:

   * Una promozione è un componente basato su pagina che viene creato/modificato con la console Siti web e memorizzato in:

     `/content/campaigns`

   * Offerta promozioni:

      * Una priorità
      * Un percorso del gestore delle promozioni

   * È possibile collegare le promozioni a una campagna per definirne data/ora di attivazione/disattivazione.
   * Puoi collegare le promozioni a un’esperienza per definirne i segmenti.
   * Le promozioni non collegate a un’esperienza non si attivano da sole, ma possono comunque essere attivate da un voucher.
   * Il componente Promozione ( `/libs/commerce/components/promotion`) contiene:

      * renderer e finestre di dialogo per l&#39;amministrazione della promozione
      * sottocomponenti per il rendering e la modifica dei parametri di configurazione specifici dei gestori di promozioni

   * Sono forniti due gestori di promozioni:

      * `DiscountPromotionHandler`, che applica uno sconto assoluto o percentuale a livello di carrello
      * `PerfectPartnerPromotionHandler`, che applica uno sconto assoluto o percentuale sul prodotto, se il prodotto partner si trova anche nel carrello

   * Il ClientContext `SegmentMgr` risolve segmenti e ClientContext `CartMgr` risolve le promozioni. Ogni promozione soggetta ad almeno un segmento risolto verrà attivata.

      * Le Promozioni Attivate vengono rimandate al server tramite una chiamata AJAX per ricalcolare il carrello.
      * Nel pannello ClientContext vengono visualizzate anche le promozioni attivate (e i voucher aggiunti).

L&#39;aggiunta o la rimozione di un voucher da un carrello viene eseguita tramite `CommerceSession` API:

```java
/**
 * Apply a voucher to this session's cart.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void addVoucher(String code) throws CommerceException;

/**
 * Remove a voucher that was previously added with {@link #addVoucher(String)}.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void removeVoucher(String code) throws CommerceException;

/**
 * Get a list of vouchers that were added to this cart via {@link #addVoucher(String)}.
 *
 * @throws CommerceException
 */
public List<Voucher> getVouchers() throws CommerceException;
```

In questo modo, il `CommerceSession` è responsabile della verifica dell&#39;esistenza e della possibilità di applicare un voucher. Questo potrebbe essere per i voucher che possono essere applicati solo se viene soddisfatta una determinata condizione; ad esempio, quando il prezzo totale del carrello è superiore a 100 $). Se un voucher non può essere applicato per alcun motivo, il `addVoucher` genererà un&#39;eccezione. Inoltre, il `CommerceSession` è responsabile dell&#39;aggiornamento dei prezzi del carrello dopo l&#39;aggiunta o la rimozione di un voucher.

Il `Voucher` è una classe bean-like che contiene campi per:

* Codice voucher
* Breve descrizione
* Riferimento alla promozione correlata che indica il tipo e il valore dello sconto

Il `AbstractJcrCommerceSession` fornito può applicare i voucher. I voucher restituiti dalla classe `getVouchers()` sono istanze di `cq:Page` contenente un nodo jcr:content con le seguenti proprietà (tra le altre):

* `sling:resourceType` (Stringa) - questo deve essere `commerce/components/voucher`

* `jcr:title` (Stringa) - per la descrizione del voucher
* `code` (Stringa) - il codice che l&#39;utente deve immettere per applicare questo voucher
* `promotion` (Stringa) - la promozione da applicare; ad esempio, `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

I gestori delle promozioni sono servizi OSGi che modificano il carrello. Il carrello supporterà diversi hook che saranno definiti nel `PromotionHandler` di rete.

```java
/**
 * Apply promotion to a cart line item. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @param cartEntry The cart line item
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyCartEntryPromotion(CommerceSession commerceSession,
                                         Promotion promotion, CartEntry cartEntry)
    throws CommerceException;

/**
 * Apply promotion to an order. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyOrderPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

public PriceInfo applyShippingPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

/**
 * Allows a promotion handler to define a custom, author-oriented message for a promotion.
 * The {@link com.adobe.cq.commerce.common.promotion.PerfectPartnerPromotionHandler}, for instance,
 * uses this to list the qualifying pairs of products in the current cart.
 * @param commerceSession
 * @param promotion
 * @return A message to display
 * @throws CommerceException
 */
public String getMessage(SlingHttpServletRequest request, CommerceSession commerceSession, Promotion promotion) throws CommerceException;

/**
 * Informs the promotion handler that something under the promotions root has been edited, and the handler
 * should invalidate any caches it might be keeping.
 */
public void invalidateCaches();
```

Sono disponibili tre gestori di promozioni:

* `DiscountPromotionHandler` applica uno sconto assoluto o percentuale a livello di carrello
* `PerfectPartnerPromotionHandler` applica uno sconto assoluto o percentuale sul prodotto se anche il partner è nel carrello
* `FreeShippingPromotionHandler` applica spedizione gratuita
