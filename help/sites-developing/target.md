---
title: Sviluppo per contenuti mirati
seo-title: Sviluppo per contenuti mirati
description: Argomenti sullo sviluppo di componenti da utilizzare con il targeting dei contenuti
seo-description: Argomenti sullo sviluppo di componenti da utilizzare con il targeting dei contenuti
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 0%

---

# Sviluppo per contenuti mirati{#developing-for-targeted-content}

Questa sezione descrive argomenti sullo sviluppo di componenti da utilizzare con il targeting dei contenuti.

* Per informazioni sulla connessione con Adobe Target, consulta [Integrazione con Adobe Target](/help/sites-administering/target.md).
* Per informazioni sulla creazione di contenuti di destinazione, consulta [Creazione di contenuti di destinazione utilizzando la modalità di targeting](/help/sites-authoring/content-targeting-touch.md).

>[!NOTE]
>
>Quando esegui il targeting di un componente AEM autore, il componente effettua una serie di chiamate lato server ad Adobe Target per registrare la campagna, impostare le offerte e recuperare i segmenti Adobe Target (se configurati). Da AEM pubblicazione ad Adobe Target non vengono effettuate chiamate lato server.

## Abilitazione del targeting con Adobe Target sulle pagine {#enabling-targeting-with-adobe-target-on-your-pages}

Per utilizzare componenti di destinazione nelle pagine che interagiscono con Adobe Target, includi nell’elemento &lt;head> un codice specifico lato client.

### Sezione testa {#the-head-section}

Aggiungi entrambi i seguenti blocchi di codice alla sezione &lt;head> della pagina:

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

Questo codice aggiunge gli oggetti javascript di analytics richiesti e carica le librerie dei servizi cloud associate al sito web. Per il servizio Target, le librerie vengono caricate tramite `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

Il set di librerie caricato dipende dal tipo di libreria client target (mbox.js o at.js) utilizzata nella configurazione di Target:

**Per mbox.js predefinito**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**Per mbox.js personalizzato**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**Per at.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>È supportata solo la versione di `at.js` fornita con il prodotto. La versione di `at.js` fornita con il prodotto può essere ottenuta guardando il file `at.js` sul posto:
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**Per at.js personalizzato**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

La funzionalità di Target sul lato client viene gestita dall&#39;oggetto `CQ_Analytics.TestTarget` . Pertanto, la pagina conterrà un codice init, come nell’esempio seguente:

```
<script type="text/javascript">
            if ( !window.CQ_Analytics ) {
                window.CQ_Analytics = {};
            }
            if ( !CQ_Analytics.TestTarget ) {
                CQ_Analytics.TestTarget = {};
            }
            CQ_Analytics.TestTarget.clientCode = 'my_client_code';
        </script>
      ...

    <div class="cloudservice testandtarget">
  <script type="text/javascript">
  CQ_Analytics.TestTarget.maxProfileParams = 11;

  if (CQ_Analytics.CCM) {
   if (CQ_Analytics.CCM.areStoresInitialized) {
    CQ_Analytics.TestTarget.registerMboxUpdateCalls();
   } else {
    CQ_Analytics.CCM.addListener("storesinitialize", function (e) {
     CQ_Analytics.TestTarget.registerMboxUpdateCalls();
    });
   }
  } else {
   // client context not there, still register calls
   CQ_Analytics.TestTarget.registerMboxUpdateCalls();
  }
  </script>
 </div>
```

Il JSP aggiunge gli oggetti JavaScript di analisi richiesti e i riferimenti alle librerie javascript lato client. Il file testandtarget.js contiene le funzioni mbox.js . L&#39;HTML generato dallo script è simile all&#39;esempio seguente:

```xml
<script type="text/javascript">
        if ( !window.CQ_Analytics ) {
            window.CQ_Analytics = {};
        }
        if ( !CQ_Analytics.TestTarget ) {
            CQ_Analytics.TestTarget = {};
        }
        CQ_Analytics.TestTarget.clientCode = 'MyClientCode';
</script>
<link rel="stylesheet" href="/etc/clientlibs/foundation/testandtarget/testandtarget.css" type="text/css">
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/testandtarget.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/init.js"></script>
```

#### Sezione corpo (inizio) {#the-body-section-start}

Aggiungi il codice seguente immediatamente dopo il tag &lt;body> per aggiungere alla pagina le funzioni del contesto client:

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### Sezione corpo (fine) {#the-body-section-end}

Aggiungi il codice seguente immediatamente prima del tag finale &lt;/body> :

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

Lo script JSP di questo componente genera chiamate all’API javascript di Target e implementa altre configurazioni richieste. L&#39;HTML generato dallo script è simile all&#39;esempio seguente:

```xml
<div class="servicecomponents cloudservices">
  <div class="cloudservice testandtarget">
    <script type="text/javascript">
      CQ_Analytics.TestTarget.maxProfileParams = 11;
      CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
        CQ_Analytics.TestTarget.registerMboxUpdateCalls();
      });
    </script>
    <div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
      <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
    </div>
    <script type="text/javascript">
      $CQ(function(){
      if( CQ_Analytics &&
          CQ_Analytics.ClientContextMgr &&
          !CQ_Analytics.ClientContextMgr.isConfigLoaded )
        {
          $CQ("#cq-analytics-texthint").show();
        }
      });
    </script>
  </div>
</div>
```

### Utilizzo di un file di libreria di Target personalizzato {#using-a-custom-target-library-file}

>[!NOTE]
>
>Se non utilizzi DTM o un altro sistema di marketing di destinazione, puoi utilizzare file di libreria di destinazione personalizzati.

>[!NOTE]
>
>Per impostazione predefinita, le mbox sono nascoste; questo comportamento è determinato dalla classe mboxDefault . Nascondere le mbox assicura che i visitatori non vedano il contenuto predefinito prima che venga scambiato; tuttavia, nascondere le mbox influisce sulle prestazioni percepite.

Il file mbox.js predefinito utilizzato per creare mbox si trova in /etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js. Per utilizzare un file mbox.js del cliente, aggiungi il file alla configurazione cloud di Target. Per aggiungere il file , il file mbox.js deve essere disponibile nel file system .

Ad esempio, se desideri utilizzare il servizio [ID Marketing Cloud](https://docs.adobe.com/content/help/en/id-service/using/home.html), devi scaricare mbox.js in modo che contenga il valore corretto per la variabile `imsOrgID`, basata sul tenant. Questa variabile è necessaria per l&#39;integrazione con il servizio ID Marketing Cloud. Per informazioni, consulta [Adobe Analytics come origine per la generazione di rapporti per Adobe Target](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) e [Prima di implementare](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/before-implement.html).

>[!NOTE]
>
>Se una mbox personalizzata è definita in una configurazione di Target, tutti devono avere accesso in lettura a **/etc/cloudservices** sui server di pubblicazione. Senza questo accesso, il caricamento dei file mbox.js sul sito web di pubblicazione genera un errore 404.

1. Vai alla pagina CQ **Strumenti** e seleziona **Cloud Services**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. Nella struttura, seleziona Adobe Target e fai doppio clic sulla configurazione di Target nell’elenco delle configurazioni.
1. Nella pagina di configurazione, fai clic su Modifica.
1. Per la proprietà Custom mbox.js , fai clic su Sfoglia e seleziona il file .
1. Per applicare le modifiche, immetti la password del tuo account Adobe Target, fai clic su Riconnetti a Target e fai clic su OK quando la connessione ha esito positivo. Quindi fare clic su OK nella finestra di dialogo Modifica componente.

La configurazione di Target include un file mbox.js personalizzato, [il codice richiesto nella sezione head](/help/sites-developing/target.md#p-the-head-section-p) della pagina aggiunge il file al framework della libreria client invece di un riferimento alla libreria testandtarget.js.

## Disabilitazione del comando Target per i componenti {#disabling-the-target-command-for-components}

La maggior parte dei componenti può essere convertita in componenti di destinazione utilizzando il comando Target nel menu di scelta rapida.

![chlimage_1-21](assets/chlimage_1-21.png)

Per rimuovere il comando Target dal menu di scelta rapida, aggiungi la seguente proprietà al nodo cq:editConfig del componente:

* Nome: cq:disableTargeting
* Tipo: booleano
* Valore: True

Ad esempio, per disabilitare il targeting per i componenti titolo delle pagine di Geometrixx Demo Site, aggiungi la proprietà al nodo /apps/geometrixx/components/title/cq:editConfig .

![chlimage_1-22](assets/chlimage_1-22.png)

## Invio di informazioni di conferma dell’ordine ad Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>Se non utilizzi DTM, invia la conferma dell’ordine ad Adobe Target.

Per tenere traccia delle prestazioni del sito web, invia ad Adobe Target le informazioni di acquisto dalla pagina di conferma dell’ordine. (Consulta [Creare una mbox orderConfirmPage](https://docs.adobe.com/content/help/en/dtm/implementing/target/configure-target/mboxes/order-confirmation-mbox.html) nella documentazione di Adobe Target.) Adobe Target riconosce i dati mbox come dati di conferma dell&#39;ordine quando il nome della MBox è `orderConfirmPage` e utilizza i seguenti nomi di parametri specifici:

* productPurchasedId: Elenco di ID che identificano i prodotti acquistati.
* orderId: ID dell&#39;ordine.
* orderTotal: Importo totale dell&#39;acquisto.

Il codice sulla pagina HTML di cui è stato effettuato il rendering che crea la mbox è simile al seguente esempio:

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

I valori di ciascun parametro sono diversi per ciascun ordine. Pertanto, è necessario un componente che generi il codice in base alle proprietà dell’acquisto. Il CQ [eCommerce Integration Framework](/help/commerce/cif-classic/administering/ecommerce.md) consente di integrarsi con il catalogo dei prodotti e implementare un carrello e una pagina per il pagamento.

L’esempio di Geometrixx Outdoors mostra la seguente pagina di conferma quando un visitatore acquista prodotti:

![chlimage_1-23](assets/chlimage_1-23.png)

Il codice seguente per lo script JSP di un componente accede alle proprietà del carrello e quindi stampa il codice per la creazione della mbox.

```java
<%--

  confirmationmbox component.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
          import="com.adobe.cq.commerce.api.CommerceService,
                  com.adobe.cq.commerce.api.CommerceSession,
                  com.adobe.cq.commerce.common.PriceFilter,
                  com.adobe.cq.commerce.api.Product,
                  java.util.List, java.util.Iterator"%><%

/* obtain the CommerceSession object */
CommerceService commerceservice = resource.adaptTo(CommerceService.class);
CommerceSession session = commerceservice.login(slingRequest, slingResponse);

/* obtain the cart items */
List<CommerceSession.CartEntry> entries = session.getCartEntries();
Iterator<CommerceSession.CartEntry> cartiterator = entries.iterator();

/* iterate the items and get the product IDs */
String productIDs = new String();
while(cartiterator.hasNext()){
 CommerceSession.CartEntry entry = cartiterator.next();
 productIDs = productIDs + entry.getProduct().getSKU();
    if (cartiterator.hasNext()) productIDs = productIDs + ", ";
}

/* get the cart price and orderID */
String total = session.getCartPrice(new PriceFilter("CART", "PRE_TAX"));
String orderID = session.getOrderId();

%><div class="mboxDefault"></div>
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=<%= productIDs %>',
     'orderId=<%= orderID %>',
     'orderTotal=<%= total %>');
</script>
```

Quando il componente è incluso nella pagina di pagamento dell’esempio precedente, l’origine pagina include il seguente script che crea la mbox:

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## Informazioni sul componente Target {#understanding-the-target-component}

Il componente Target consente agli autori di creare mbox dinamiche dai componenti di contenuto CQ. (Consulta [Targeting dei contenuti](/help/sites-authoring/content-targeting-touch.md).) Il componente Target si trova in /libs/cq/personalization/components/target.

Lo script target.jsp accede alle proprietà della pagina per determinare il motore di destinazione da utilizzare per il componente, quindi esegue lo script appropriato:

* Adobe Target: /libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target con AT.JS](/help/sites-administering/target.md): /libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md): /libs/cq/personalization/components/target/engine_cq_campaign.jsp
* Regole lato client/ContextHub: /libs/cq/personalization/components/target/engine_cq.jsp

### Creazione di mbox {#the-creation-of-mboxes}

>[!NOTE]
>
>Per impostazione predefinita, le mbox sono nascoste; questo comportamento è determinato dalla classe mboxDefault . Nascondere le mbox assicura che i visitatori non vedano il contenuto predefinito prima che venga scambiato; tuttavia, nascondere le mbox influisce sulle prestazioni percepite.

Quando Adobe Target guida il targeting del contenuto, lo script engine_tnt.jsp crea mbox che contengono il contenuto dell&#39;esperienza di destinazione:

* Aggiunge un elemento `div` con la classe `mboxDefault`, come richiesto dall’API di Adobe Target.

* Aggiunge il contenuto mbox (il contenuto dell’esperienza di destinazione) all’interno dell’elemento `div` .

Dopo l’elemento `mboxDefault` div , viene inserito il codice javascript che crea la mbox:

* Il nome mbox, l’ID e la posizione si basano sul percorso dell’archivio del componente.
* Lo script ottiene i nomi e i valori dei parametri Client Context.
* Vengono effettuate chiamate alle funzioni definite da mbox.js e da altre librerie client per creare mbox.

#### Librerie client per il targeting dei contenuti {#client-libraries-for-content-targeting}

Di seguito sono riportate le categorie clientlib disponibili:

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
