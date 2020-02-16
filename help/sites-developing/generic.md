---
title: Sviluppo (generico)
seo-title: Sviluppo (generico)
description: Il framework di integrazione include un livello di integrazione con un’API, che consente di creare componenti AEM per le funzionalità eCommerce
seo-description: Il framework di integrazione include un livello di integrazione con un’API, che consente di creare componenti AEM per le funzionalità eCommerce
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: d8ee3b57-633a-425e-bf36-646f0e0bad52
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16

---


# Sviluppo (generico){#developing-generic}

>[!NOTE]
>
>[È disponibile anche la documentazione](/help/sites-developing/ecommerce.md#api-documentation) API.

Il framework di integrazione include un livello di integrazione con un&#39;API. Questo consente di creare componenti AEM per funzionalità eCommerce (indipendentemente dal motore eCommerce specifico). Consente inoltre di utilizzare il database CRX interno o di collegare un sistema eCommerce ed estrarre i dati del prodotto in AEM.

Per usare il livello di integrazione, sono disponibili diversi componenti AEM forniti con il prodotto. Attualmente questi sono:

* Un componente per la visualizzazione di un prodotto
* Un carrello
* Promozioni e voucher
* Progetti di catalogo e sezioni
* Check-out
* Ricerca

Per la ricerca viene fornito un gancio di integrazione che consente di utilizzare la ricerca AEM, una ricerca di terze parti (come Search&amp;Promote) o una combinazione di questi.

## Selezione motore eCommerce {#ecommerce-engine-selection}

Il framework eCommerce può essere utilizzato con qualsiasi soluzione eCommerce. Il motore utilizzato deve essere identificato da AEM, anche quando si utilizza il motore generico AEM:

* I motori di eCommerce sono servizi OSGi che supportano l&#39; `CommerceService` interfaccia

   * I motori possono essere distinti da una proprietà `commerceProvider` del servizio

* AEM supporta `Resource.adaptTo()` per `CommerceService` e `Product`

   * L&#39; `adaptTo` implementazione cerca una `cq:commerceProvider` proprietà nella gerarchia della risorsa:

      * Se trovato, il valore viene utilizzato per filtrare la ricerca del servizio commerce.
      * Se non viene trovato, viene utilizzato il servizio di commercio di livello più elevato.
   * Viene utilizzato un `cq:Commerce` mixin per `cq:commerceProvider` aggiungere risorse fortemente tipizzate.


* La `cq:commerceProvider` proprietà viene utilizzata anche per fare riferimento alla definizione di fabbrica commerciale appropriata.

   * Ad esempio, una `cq:commerceProvider` proprietà con il valore geometrixx sarà correlata alla configurazione OSGi per **Day CQ Commerce Factory for Geometrixx-Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`), dove `commerceProvider` anche il parametro ha il valore `geometrixx`.
   * In questo caso è possibile configurare ulteriori proprietà (se appropriato e disponibile).

In un’installazione standard di AEM è necessaria un’implementazione specifica, ad esempio:

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | esempio geometrixx; ciò include estensioni minime per l&#39;API generica |

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
>Con CRXDE Lite potete vedere come questo viene gestito nel componente prodotto per l’implementazione generica di AEM:
>
>`/apps/geometrixx-outdoors/components/product`

### Gestione sessione {#session-handling}

Una sessione per memorizzare le informazioni relative al carrello acquisti del cliente.

The **CommerceSession**:

* Possiede il **carrello**

   * esegue add/remove/etc
   * esegue i vari calcoli sul carrello;

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Possiede la persistenza dei dati dell&#39; **ordine** :

   `CommerceSession.getUserContext()`

* Può recuperare/aggiornare i dettagli di consegna utilizzando `updateOrder(Map<String, Object> delta)`
* Possiede anche la connessione di elaborazione **pagamento**
* Possiede anche la connessione di **evasione**

### Architettura {#architecture}

#### Architettura di prodotti e varianti {#architecture-of-product-and-variants}

Un singolo prodotto può presentare più varianti; ad esempio, può variare in base al colore e/o alla dimensione. Un prodotto deve definire quali proprietà determinano la variazione; chiamiamo questi assi ** varianti.

Tuttavia, non tutte le proprietà sono assi variabili. Le variazioni possono interessare anche altre proprietà; ad esempio, il prezzo potrebbe dipendere dalle dimensioni. Queste proprietà non possono essere selezionate dall&#39;acquirente e pertanto non sono considerate assi di variante.

Ciascun prodotto e/o variante è rappresentato da una risorsa e pertanto viene mappato 1:1 su un nodo del repository. È un corollario che un prodotto e/o una variante specifica possa essere identificato in modo univoco dal suo percorso.

Qualsiasi risorsa prodotto può essere rappresentata da un `Product API`. La maggior parte delle chiamate nell&#39;API del prodotto sono specifiche per le varianti (anche se le variazioni possono ereditare valori condivisi da un predecessore), ma ci sono anche chiamate che elencano il set di variazioni ( `getVariantAxes()`, `getVariants()`ecc.).

>[!NOTE]
>
>In effetti, gli assi di una variante sono determinati da qualsiasi `Product.getVariantAxes()` risultato:
>
>* per l’implementazione generica, AEM la legge da una proprietà nei dati del prodotto ( `cq:productVariantAxes`)
>
>
Mentre i prodotti (in generale) possono avere molti assi di variante, il componente prodotto out-of-the-box gestisce solo due:
>
>1. `size`
   >
   >
1. più uno
   >   Questa variante aggiuntiva viene selezionata tramite la `variationAxis` proprietà del riferimento prodotto (in genere `color` per Geometrixx Outdoors).
>



#### Riferimenti prodotto e dati PIM {#product-references-and-pim-data}

In generale:

* I dati PIM si trovano in `/etc`

* Riferimenti ai prodotti in `/content`.

Deve essere presente una mappa 1:1 tra le varianti di prodotto e i nodi dati del prodotto.

Anche i riferimenti ai prodotti devono avere un nodo per ogni variante presentata, ma non è necessario presentare tutte le varianti. Ad esempio, se un prodotto ha varianti S, M, L, i dati del prodotto potrebbero essere:

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

Mentre un catalogo &quot;Big and Tall&quot; può contenere solo:

```shell
content
  big-and-tall
    shirt
      shirt-l
```

Infine, non è previsto l&#39;uso di dati di prodotto. È possibile inserire tutti i dati di prodotto sotto i riferimenti nel catalogo; ma non è possibile avere più cataloghi senza duplicare tutti i dati del prodotto.

**API**

#### com.adobe.cq.comCommerce.api.Interfaccia prodotto {#com-adobe-cq-commerce-api-product-interface}

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

* **Meccanismo di storage generale**

   * I nodi di prodotto non sono:non strutturati.
   * Un nodo prodotto può essere:

      * Un riferimento, con i dati del prodotto memorizzati altrove:

         * I riferimenti ai prodotti contengono una `productData` proprietà che fa riferimento ai dati del prodotto (in genere sotto `/etc/commerce/products`).
         * I dati del prodotto sono gerarchici; gli attributi del prodotto vengono ereditati dagli predecessori di un nodo di dati di prodotto.
         * I riferimenti ai prodotti possono anche contenere proprietà locali, che ignorano quelle specificate nei relativi dati di prodotto.
      * Un prodotto:

         * Senza una `productData` proprietà.
         * Un nodo di prodotto che contiene tutte le proprietà localmente (e non contiene una proprietà productData) eredita gli attributi di prodotto direttamente dai propri predecessori.


* **Struttura di prodotto generica AEM**

   * Ogni variante deve avere un proprio nodo foglia.
   * L&#39;interfaccia del prodotto rappresenta sia prodotti che varianti, ma il nodo del repository correlato è specifico sul quale si trova.
   * Il nodo product descrive gli attributi del prodotto e gli assi delle varianti.

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

* Il carrello è di proprietà del `CommerceSession:`

   * Consente di `CommerceSession` eseguire operazioni di aggiunta, rimozione ecc.
   * Vengono `CommerceSession` inoltre eseguiti i vari calcoli sul carrello.
   * Vengono `CommerceSession` inoltre applicati voucher e promozioni che sono stati licenziati al carrello.

* Anche se non direttamente correlati al carrello, il `CommerceSession` cliente deve anche fornire informazioni sui prezzi del catalogo (dal momento che possiede i prezzi)

   * La determinazione prezzi può avere diversi modificatori:

      * Sconti sulla quantità.
      * Valute diverse.
      * IVA e IVA.
   * I modificatori sono completamente aperti con la seguente interfaccia:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**Archiviazione**

* Archiviazione

   * In AEM i carrelli di maiuscole e minuscole generici sono memorizzati in [ClientContext](/help/sites-administering/client-context.md)

**Personalizzazione**

* La personalizzazione deve sempre essere guidata da [ClientContext](/help/sites-administering/client-context.md).
* ClientContext `/version/` del carrello viene creato in tutti i casi:

   * I prodotti devono essere aggiunti utilizzando il `CommerceSession.addCartEntry()` metodo .

* Esempio di informazioni sul carrello nel carrello ClientContext:

![chlimage_1-33](assets/chlimage_1-33a.png)

#### Architettura del Checkout {#architecture-of-checkout}

**Dati carrello e ordine**

La proprietà `CommerceSession` possiede i tre elementi:

1. **Contenuto del carrello**

   Lo schema del contenuto del carrello è fisso dall&#39;API:

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **Prezzi**

   Lo schema tariffario è anche fissato dall&#39;API:

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **Dettagli ordine**

   Tuttavia, i dettagli dell&#39;ordine *non* vengono corretti dall&#39;API:

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**Calcoli di spedizione**

* I moduli di ordine spesso devono presentare più opzioni di spedizione (e prezzi).
* I prezzi possono essere basati su articoli e dettagli dell&#39;ordine, come peso e/o indirizzo di consegna.
* L&#39; `CommerceSession` utente ha accesso a tutte le dipendenze, quindi può essere trattato in modo simile al prezzo del prodotto:

   * Il `CommerceSession` proprietario del prezzo di spedizione.
   * Utilizzate `updateOrder(Map<String, Object> delta)` per recuperare/aggiornare i dettagli di consegna.

### Ricerca definizione {#search-definition}

In base al modello di API per i servizi standard, il progetto eCommerce fornisce un set di API relative alla ricerca che possono essere implementate dai singoli motori di commercio.

>[!NOTE]
>
>Attualmente, solo il motore ibrido implementa l&#39;API di ricerca out-of-the-box.
>
>Tuttavia, l&#39;API di ricerca è generica e può essere implementata da ogni CommerceService singolarmente.
>
>Pertanto, anche se l&#39;implementazione generica fornita out-of-the-box non implementa questa API, potete estenderla e aggiungere la funzionalità di ricerca.

Il progetto eCommerce contiene un componente di ricerca predefinito, che si trova in:

`/libs/commerce/components/search`

![chlimage_1-34](assets/chlimage_1-34a.png)

Questo utilizza l&#39;API di ricerca per eseguire una query sul motore di eCommerce (vedi Selezione [motore di](#ecommerce-engine-selection)eCommerce) selezionato:

#### API di ricerca {#search-api}

Il progetto principale offre diverse classi generiche / helper:

1. `CommerceQuery`

   
Viene utilizzato per descrivere una query di ricerca (contiene informazioni sul testo della query, la pagina corrente, la dimensione della pagina, l’ordinamento e i facet selezionati). Tutti i servizi eCommerce che implementano l&#39;API di ricerca riceveranno le istanze di questa classe per eseguire la ricerca. È `CommerceQuery` possibile creare un&#39;istanza di un oggetto di richiesta ( `HttpServletRequest`).

1. `FacetParamHelper`

   
È una classe di utilità che fornisce un metodo statico, `toParams` , utilizzato per generare stringhe di `GET` parametri da un elenco di facet e un valore attivato. Questa funzione è utile nell’interfaccia utente, dove è necessario visualizzare un collegamento ipertestuale per ciascun valore di ciascun facet, in modo che quando l’utente fa clic sul collegamento ipertestuale il relativo valore venga attivato (ovvero se è stato selezionato, viene rimosso dalla query, altrimenti aggiunto). Questo si occupa di tutte le logiche di gestione di facet multivalore/monomalore, valori prevalenti, ecc.

Il punto di ingresso per l&#39;API di ricerca è il `CommerceService#search` metodo che restituisce un `CommerceResult` oggetto. Per ulteriori informazioni su questo argomento, consultate la Documentazione API.

### Sviluppo di promozioni e voucher {#developing-promotions-and-vouchers}

* Voucher:

   * Un voucher è un componente basato su pagina creato/modificato con la console Siti Web e memorizzato in:

      `/content/campaigns`

   * Fornitura di voucher:

      * Un codice di voucher (che deve essere digitato nel carrello dal cliente).
      * Etichetta del voucher (da visualizzare dopo che l&#39;acquirente l&#39;ha inserita nel carrello).
      * Un percorso di promozione (che definisce l’azione applicata dal voucher).
   * I voucher non dispongono di date/ore di attivazione e disattivazione, ma utilizzano quelle delle campagne padre.
   * I motori per il commercio estero possono anche fornire buoni; tali requisiti richiedono almeno:

      * Un codice voucher
      * Un `isValid()` metodo
   * Il componente **Voucher** ( `/libs/commerce/components/voucher`) fornisce:

      * Un renderer per l’amministrazione del voucher; vengono visualizzati tutti i voucher attualmente presenti nel carrello.
      * Le finestre di dialogo di modifica (modulo) per l&#39;amministrazione (aggiunta/rimozione) dei voucher.
      * Azioni necessarie per aggiungere o rimuovere voucher nel carrello.



* Promozioni:

   * Una promozione è un componente basato su pagina creato/modificato con la console Siti Web e memorizzato in:

      `/content/campaigns`

   * Offerta promozionale:

      * Priorità
      * Percorso gestore di promozione
   * Potete collegare le promozioni a una campagna per definirne la data/ora di attivazione/disattivazione.
   * Puoi collegare le promozioni a un&#39;esperienza per definirne i segmenti.
   * Le promozioni non collegate a un&#39;esperienza non si attivano autonomamente, ma possono essere comunque attivate da un Voucher.
   * Il componente Promozione ( `/libs/commerce/components/promotion`) contiene:

      * renderer e finestre di dialogo per l&#39;amministrazione della promozione
      * componenti secondari per il rendering e la modifica dei parametri di configurazione specifici per i gestori della promozione
   * Due gestori di promozione vengono forniti in dotazione:

      * `DiscountPromotionHandler`, che applica uno sconto assoluto o percentuale a livello di carrello
      * `PerfectPartnerPromotionHandler`, che applica uno sconto assoluto o percentuale di prodotto se il prodotto partner è anche nel carrello
   * ClientContext `SegmentMgr` risolve i segmenti e ClientContext `CartMgr` risolve le promozioni. Ogni promozione soggetta ad almeno un segmento risolto verrà attivata.

      * Le promozioni generate vengono inviate al server tramite una chiamata AJAX per ricalcolare il carrello.
      * Le promozioni con attivazione (e i voucher aggiunti) vengono visualizzate anche nel pannello ClientContext.




L&#39;aggiunta o la rimozione di un voucher da un carrello viene eseguita tramite l&#39; `CommerceSession` API:

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

In questo modo, `CommerceSession` è responsabile verificare se un voucher esiste e se può essere applicato o meno. Questo potrebbe essere per i voucher che possono essere applicati solo se è soddisfatta una determinata condizione; ad esempio, quando il prezzo totale del carrello è maggiore di $100). Se un voucher non può essere applicato per alcun motivo, il `addVoucher` metodo genererà un&#39;eccezione. Inoltre, l&#39; `CommerceSession` utente è responsabile dell&#39;aggiornamento dei prezzi del carrello dopo l&#39;aggiunta o la rimozione di un voucher.

Si `Voucher` tratta di una classe simile a una fava che contiene campi per:

* Codice voucher
* Breve descrizione
* Riferimento alla promozione correlata che indica il tipo di sconto e il valore

I voucher `AbstractJcrCommerceSession` forniti possono essere applicati. I voucher restituiti dalla classe `getVouchers()` sono istanze di `cq:Page` contenitore di un nodo jcr:content con le seguenti proprietà (tra le altre):

* `sling:resourceType` (String) - deve essere `commerce/components/voucher`

* `jcr:title` (Stringa) - per la descrizione del voucher
* `code` (Stringa) - il codice che l&#39;utente deve immettere per applicare questo voucher
* `promotion` (String) - la promozione da applicare;ad esempio `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

I gestori di promozione sono servizi OSGi che modificano il carrello. Il carrello supporterà diversi ganci che saranno definiti nell&#39; `PromotionHandler` interfaccia.

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

