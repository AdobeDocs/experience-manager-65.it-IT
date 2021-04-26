---
title: Sviluppo (generico)
seo-title: Sviluppo (generico)
description: Il framework di integrazione include un livello di integrazione con un’API che consente di creare componenti AEM per le funzionalità di eCommerce
seo-description: Il framework di integrazione include un livello di integrazione con un’API che consente di creare componenti AEM per le funzionalità di eCommerce
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---

# Sviluppo (generico){#developing-generic}

>[!NOTE]
>
>[È disponibile anche la ](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) documentazione API .

Il framework di integrazione include un livello di integrazione con un’API. Questo ti consente di creare componenti AEM per le funzionalità di eCommerce (indipendentemente dal motore di eCommerce specifico). Consente inoltre di utilizzare il database CRX interno o di collegare un sistema eCommerce ed estrarre i dati dei prodotti in AEM.

Per utilizzare il livello di integrazione, sono disponibili diversi componenti AEM pronti all’uso. Attualmente questi sono:

* Componente di visualizzazione del prodotto
* Un carrello
* Promozioni e buoni
* Blueprint di catalogo e di sezione
* Check-out
* Ricerca

Per la ricerca viene fornito un gancio di integrazione che consente di utilizzare la ricerca AEM, una ricerca di terze parti (come Search&amp;Promote) o una combinazione di essi.

## Selezione del motore di e-commerce {#ecommerce-engine-selection}

Il framework eCommerce può essere utilizzato con qualsiasi soluzione eCommerce, il motore utilizzato deve essere identificato da AEM, anche quando si utilizza il motore generico AEM:

* I motori eCommerce sono servizi OSGi che supportano l&#39;interfaccia `CommerceService`

   * I motori possono essere distinti da una proprietà del servizio `commerceProvider`

* AEM supporta `Resource.adaptTo()` per `CommerceService` e `Product`

   * L’implementazione `adaptTo` cerca una proprietà `cq:commerceProvider` nella gerarchia della risorsa:

      * Se trovato, il valore viene utilizzato per filtrare la ricerca del servizio commerce.
      * Se non viene trovato, viene utilizzato il servizio di e-commerce più alto.
   * Viene utilizzato un mixin `cq:Commerce` per aggiungere il `cq:commerceProvider` alle risorse fortemente tipizzate.


* La proprietà `cq:commerceProvider` viene utilizzata anche per fare riferimento alla definizione corretta di commerce factory.

   * Ad esempio, una proprietà `cq:commerceProvider` con il valore geometrixx sarà correlata alla configurazione OSGi per **Day CQ Commerce Factory for Geometrixx-Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`) - dove il parametro `commerceProvider` ha anche il valore `geometrixx`.
   * Qui è possibile configurare altre proprietà (quando appropriato e disponibile).

In un’installazione AEM standard è necessaria un’implementazione specifica, ad esempio:

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | esempio geometrixx; questo include estensioni minime per l’API generica |

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
>Utilizzando CRXDE Lite puoi vedere come viene gestita nel componente prodotto per l’implementazione generica AEM:
>
>`/apps/geometrixx-outdoors/components/product`

### Gestione delle sessioni {#session-handling}

Una sessione per memorizzare le informazioni relative al carrello acquisti del cliente.

**CommerceSession**:

* Possiede il **carrello**

   * esegue add/remove/etc
   * esegue i vari calcoli sul carrello;

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Possiede la persistenza dei dati **order**:

   `CommerceSession.getUserContext()`

* Può recuperare/aggiornare i dettagli di consegna utilizzando `updateOrder(Map<String, Object> delta)`
* Possiede anche la connessione di elaborazione **pagamento**
* Possiede anche la connessione **compiment**

### Architettura {#architecture}

#### Architettura di prodotti e varianti {#architecture-of-product-and-variants}

Un singolo prodotto può presentare più varianti; ad esempio, potrebbe variare a seconda del colore e/o della dimensione. Un prodotto deve definire quali proprietà determinano la variazione; chiamiamo questi *assi di variante*.

Tuttavia, non tutte le proprietà sono assi variabili. Le varianti possono influenzare anche altre proprietà; ad esempio, il prezzo potrebbe dipendere dalle dimensioni. Queste proprietà non possono essere selezionate dall&#39;acquirente e quindi non sono considerate assi di variante.

Ogni prodotto e/o variante è rappresentato da una risorsa e pertanto viene mappato 1:1 su un nodo di archivio. È un corollario che un prodotto e/o variante specifico possa essere identificato in modo univoco dal suo percorso.

Qualsiasi risorsa di prodotto può essere rappresentata da un `Product API`. La maggior parte delle chiamate nell&#39;API del prodotto sono specifiche per le varianti (anche se le varianti potrebbero ereditare valori condivisi da un predecessore), ma ci sono anche chiamate che elencano il set di varianti ( `getVariantAxes()`, `getVariants()`, ecc.).

>[!NOTE]
>
>In effetti, un asse di variante è determinato da qualsiasi valore restituito da `Product.getVariantAxes()`:
>
>* per l&#39;implementazione generica AEM la legge da una proprietà nei dati del prodotto ( `cq:productVariantAxes`)
>
>
Mentre i prodotti (in generale) possono avere molti assi di variante, il componente di prodotto preconfigurato gestisce solo due elementi:
>
>1. `size`
>1. più uno

>
>   
Questa variante aggiuntiva viene selezionata tramite la proprietà `variationAxis` del riferimento al prodotto (in genere `color` per Geometrixx Outdoors).

#### Riferimenti prodotto e dati PIM {#product-references-and-pim-data}

In generale:

* I dati PIM si trovano in `/etc`

* Riferimenti ai prodotti in `/content`.

Deve essere presente una mappa 1:1 tra le varianti di prodotto e i nodi di dati di prodotto.

I riferimenti al prodotto devono avere anche un nodo per ogni variante presentata - ma non è necessario presentare tutte le varianti. Ad esempio, se un prodotto presenta varianti S, M, L, i dati del prodotto potrebbero essere:

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

Mentre un catalogo &quot;Grande e alto&quot; potrebbe avere solo:

```shell
content
  big-and-tall
    shirt
      shirt-l
```

Infine, non vi è alcun obbligo di utilizzare i dati dei prodotti. È possibile inserire tutti i dati di prodotto sotto i riferimenti nel catalogo; ma non puoi avere più cataloghi senza duplicare tutti i dati dei prodotti.

**API**

#### com.adobe.cq.commerce.api.Interfaccia prodotto {#com-adobe-cq-commerce-api-product-interface}

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

#### com.adobe.cq.commerce.api.VariantFilter {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * e.g. when using {@link Product#getVariants(VariantFilter filter)}.
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

   * I nodi di prodotto non sono:non strutturati.
   * Un nodo di prodotto può essere:

      * Un riferimento con i dati dei prodotti memorizzati altrove:

         * I riferimenti al prodotto contengono una proprietà `productData` che fa riferimento ai dati del prodotto (in genere in `/etc/commerce/products`).
         * I dati del prodotto sono gerarchici; gli attributi di prodotto vengono ereditati dagli predecessori di un nodo di dati di prodotto.
         * I riferimenti ai prodotti possono anche contenere proprietà locali, che sovrascrivono quelle specificate nei relativi dati di prodotto.
      * Un prodotto:

         * Senza una proprietà `productData` .
         * Un nodo di prodotto che contiene tutte le proprietà localmente (e non contiene una proprietà productData) eredita gli attributi di prodotto direttamente dai propri predecessori.


* **Struttura del prodotto AEM-generico**

   * Ogni variante deve avere un proprio nodo foglia.
   * L’interfaccia del prodotto rappresenta sia i prodotti che le varianti, ma il nodo di archivio correlato è specifico a riguardo.
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

   * `CommerceSession` esegue l&#39;aggiunta, la rimozione, ecc.
   * Il `CommerceSession` esegue anche i vari calcoli sul carrello.
   * Il `CommerceSession` applica anche voucher e promozioni inviate al carrello.

* Sebbene non sia direttamente correlato al carrello, la sezione `CommerceSession` deve anche fornire informazioni sui prezzi di catalogo (in quanto possiede i prezzi)

   * I prezzi possono avere diversi modificatori:

      * Sconti sulla quantità.
      * Valute diverse.
      * IVA soggetta e IVA esente.
   * I modificatori sono completamente aperti con la seguente interfaccia:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**Archiviazione**

* Archiviazione

   * Nel caso AEM-generico i carrelli di sono memorizzati nel [ClientContext](/help/sites-administering/client-context.md)

**Personalizzazione**

* La personalizzazione deve sempre essere guidata attraverso il [ClientContext](/help/sites-administering/client-context.md).
* In tutti i casi viene creato un ClientContext `/version/` del carrello:

   * I prodotti devono essere aggiunti utilizzando il metodo `CommerceSession.addCartEntry()` .

* Di seguito è riportato un esempio di informazioni sul carrello nel carrello del ClientContext:

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### Architettura del checkout {#architecture-of-checkout}

**Dati carrello e ordine**

Il `CommerceSession` possiede i tre elementi:

1. **Contenuto del carrello**

   Lo schema del contenuto del carrello è fisso dall’API:

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **Prezzi**

   Lo schema tariffario viene inoltre corretto dall’API:

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **Dettagli ordine**

   Tuttavia, i dettagli dell’ordine sono *non* corretti dall’API:

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**Calcoli di spedizione**

* I moduli di ordine spesso devono presentare più opzioni di spedizione (e prezzi).
* I prezzi possono essere basati su articoli e dettagli dell&#39;ordine, quali peso e/o indirizzo di consegna.
* Il `CommerceSession` ha accesso a tutte le dipendenze, in modo che possa essere trattato in modo simile al prezzo del prodotto:

   * Il `CommerceSession` possiede i prezzi di spedizione.
   * Utilizza `updateOrder(Map<String, Object> delta)` per recuperare/aggiornare i dettagli di consegna.

### Definizione ricerca {#search-definition}

Seguendo il modello API di servizio standard, il progetto eCommerce fornisce un set di API relative alla ricerca che possono essere implementate dai singoli motori di e-commerce.

>[!NOTE]
>
>Attualmente, solo il motore ibrido implementa l’API di ricerca preconfigurata.
>
>Tuttavia, l’API di ricerca è generica e può essere implementata singolarmente da ogni CommerceService.
>
>Pertanto, anche se l’implementazione generica fornita out-of-the-box non implementa questa API, puoi estenderla e aggiungere la funzionalità di ricerca.

Il progetto eCommerce contiene un componente di ricerca predefinito, che si trova in:

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

In questo modo si utilizza l&#39;API di ricerca per eseguire una query sul motore di e-commerce selezionato (consulta [Selezione motore di eCommerce](#ecommerce-engine-selection)):

#### API di ricerca {#search-api}

Il progetto principale prevede diverse classi generiche / helper:

1. `CommerceQuery`

   Viene utilizzato per descrivere una query di ricerca (contiene informazioni sul testo della query, sulla pagina corrente, sulle dimensioni della pagina, sull’ordinamento e sui facet selezionati). Tutti i servizi eCommerce che implementano l’API di ricerca riceveranno istanze di questa classe per eseguire la ricerca. È possibile creare un&#39;istanza di `CommerceQuery` da un oggetto di richiesta ( `HttpServletRequest`).

1. `FacetParamHelper`

   È una classe di utilità che fornisce un metodo statico - `toParams` - utilizzato per generare stringhe di parametri `GET` da un elenco di facet e un valore attivato. Questa funzione è utile sul lato dell’interfaccia utente, in cui è necessario visualizzare un collegamento ipertestuale per ogni valore di ciascun facet, in modo che quando l’utente fa clic sul collegamento ipertestuale il relativo valore venga attivato (ovvero, se è stato selezionato, viene rimosso dalla query, altrimenti aggiunto). Questo si occupa di tutte le logiche di gestione di facet con più/singoli valori, valori di override, ecc.

Il punto di ingresso per l&#39;API di ricerca è il metodo `CommerceService#search` che restituisce un oggetto `CommerceResult`. Per ulteriori informazioni su questo argomento, consulta la documentazione API .

### Sviluppo di promozioni e voucher {#developing-promotions-and-vouchers}

* Voucher:

   * Un voucher è un componente basato su pagina che viene creato/modificato con la console Siti web e memorizzato in:

      `/content/campaigns`

   * Alimentazione:

      * Un codice voucher (da inserire nel carrello dall&#39;acquirente).
      * Etichetta del voucher (da visualizzare dopo che l’acquirente l’ha inserita nel carrello).
      * Un percorso di promozione (che definisce l’azione applicata al voucher).
   * I voucher non hanno la propria data/ora di attivazione e disattivazione, ma utilizzano quelle delle campagne principali.
   * I motori per il commercio estero possono anche fornire buoni; queste richiedono almeno:

      * Un codice voucher
      * Un metodo `isValid()`
   * Il componente **Voucher** ( `/libs/commerce/components/voucher`) fornisce:

      * un trasformatore per l&#39;amministrazione dei buoni; questo mostra tutti i voucher attualmente nel carrello.
      * Le finestre di dialogo di modifica (modulo) per l’amministrazione (aggiunta/rimozione) dei voucher.
      * Azioni necessarie per aggiungere/rimuovere voucher al carrello o dal carrello.



* Promozioni:

   * Una promozione è un componente basato su pagina che viene creato/modificato con la console Siti web e memorizzato in:

      `/content/campaigns`

   * Offerta promozionale:

      * Una priorità
      * Un percorso handler di promozione
   * Puoi collegare le promozioni a una campagna per definirne la data/ora di attivazione/disattivazione.
   * Puoi collegare le promozioni a un’esperienza per definirne i segmenti.
   * Le promozioni non collegate a un’esperienza non si attivano da sole, ma possono ancora essere attivate da un Voucher.
   * Il componente Promozione ( `/libs/commerce/components/promotion`) contiene:

      * moduli di rendering e finestre di dialogo per l&#39;amministrazione delle promozioni
      * sottocomponenti per il rendering e la modifica dei parametri di configurazione specifici per i gestori della promozione
   * Sono forniti due gestori di promozione:

      * `DiscountPromotionHandler`, che applica uno sconto assoluto o percentuale a livello di carrello
      * `PerfectPartnerPromotionHandler`, che applica uno sconto assoluto o percentuale del prodotto se il prodotto partner è anche nel carrello
   * Il ClientContext `SegmentMgr` risolve i segmenti e il ClientContext `CartMgr` risolve le promozioni. Viene attivata ogni promozione soggetta ad almeno un segmento risolto.

      * Le promozioni attivate vengono rimandate al server tramite una chiamata AJAX per ricalcolare il carrello.
      * Nel pannello ClientContext vengono visualizzate anche le promozioni attive (e i voucher aggiunti).




L’aggiunta/rimozione di un voucher da un carrello viene eseguita tramite l’ `CommerceSession` API :

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

In questo modo, il `CommerceSession` è responsabile del controllo dell&#39;esistenza di un voucher e della sua applicazione o meno. Questo potrebbe essere per i buoni che possono essere applicati solo se è soddisfatta una determinata condizione; ad esempio, quando il prezzo totale del carrello è maggiore di $100). Se un voucher non può essere applicato per alcun motivo, il metodo `addVoucher` genererà un&#39;eccezione. Inoltre, il `CommerceSession` è responsabile dell&#39;aggiornamento dei prezzi del carrello dopo l&#39;aggiunta o la rimozione di un buono.

La `Voucher` è una classe simile a fagioli che contiene campi per:

* Codice voucher
* Breve descrizione
* Riferimento alla promozione correlata che indica il tipo e il valore di sconto

Il `AbstractJcrCommerceSession` fornito può applicare buoni. I voucher restituiti dalla classe `getVouchers()` sono istanze di `cq:Page` contenenti un nodo jcr:content con le seguenti proprietà (tra le altre):

* `sling:resourceType` (Stringa) - deve essere  `commerce/components/voucher`

* `jcr:title` (Stringa) - per la descrizione del voucher
* `code` (Stringa) - il codice che l&#39;utente deve immettere per applicare questo voucher
* `promotion` (Stringa) - la promozione da applicare; ad esempio  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

I gestori delle promozioni sono servizi OSGi che modificano il carrello. Il carrello supporterà diversi hook che saranno definiti nell&#39;interfaccia `PromotionHandler`.

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

Sono disponibili tre gestori di promozione:

* `DiscountPromotionHandler` applica uno sconto assoluto o percentuale a livello di carrello
* `PerfectPartnerPromotionHandler` applica uno sconto assoluto o percentuale del prodotto se il partner del prodotto è anche nel carrello
* `FreeShippingPromotionHandler` applica la spedizione gratuita
