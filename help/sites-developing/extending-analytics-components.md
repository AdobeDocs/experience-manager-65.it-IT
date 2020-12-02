---
title: Aggiunta  tracciamento Adobe Analytics ai componenti
seo-title: Aggiunta  tracciamento Adobe Analytics ai componenti
description: 'null'
seo-description: 'null'
uuid: 447b140c-678c-428d-a1c9-ecbdec75cd42
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: a11c39b4-c23b-4207-8898-33aea25f2ad0
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---


# Aggiunta  tracciamento Adobe Analytics ai componenti{#adding-adobe-analytics-tracking-to-components}

## Inclusione del modulo Adobe Analytics  in un componente Pagina {#including-the-adobe-analytics-module-in-a-page-component}

Componenti per modelli di pagina (ad esempio `head.jsp, body.jsp`) è necessario che JSP includa per caricare ContextHub e l&#39;integrazione Adobe Analytics  (che fa parte di Cloud Services). Tutto include il caricamento di file JavaScript.

La voce ContextHub deve essere inclusa immediatamente sotto il tag `<head>`, mentre gli Cloud Services devono essere inclusi nella sezione `<head>` e prima della sezione `</body>`; ad esempio:

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

Lo script `contexthub` inserito dopo l&#39;elemento `<head>` aggiunge alla pagina le funzionalità ContextHub.

Gli script `cloudservices` aggiunti nelle sezioni `<head>` e `<body>` si applicano alle configurazioni dei servizi cloud aggiunte alla pagina. Se la pagina utilizza più di una configurazione di Cloud Services, è necessario includere il jsp ContextHub e il jsp di Cloud Services solo una volta.

Quando alla pagina viene aggiunto un framework Adobe Analytics , gli script `cloudservices` generano  JavaScript correlati ad Adobe Analytics e riferimenti a librerie lato client, come nell&#39;esempio seguente:

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
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
```

Questo codice è incluso in tutti AEM siti di esempio, ad esempio Geometrixx Outdoors.

### Evento sitecatalystAfterCollect {#the-sitecatalystaftercollect-event}

Lo script `cloudservices` attiva l&#39;evento `sitecatalystAfterCollect`:

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

Questo evento viene attivato per indicare che il tracciamento della pagina è stato completato. Se state eseguendo ulteriori operazioni di tracciamento in questa pagina, dovreste ascoltare questo evento invece dell&#39;evento di caricamento del documento o pronto per il documento. L&#39;utilizzo dell&#39;evento `sitecatalystAfterCollect` evita conflitti o altri comportamenti imprevedibili.

>[!NOTE]
>
>La libreria `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` include il codice del file  Adobe Analytics `s_code.js`.

## Implementazione  tracciamento Adobe Analytics per i componenti personalizzati {#implementing-adobe-analytics-tracking-for-custom-components}

Abilitate i componenti AEM a interagire con il framework Adobe Analytics . Quindi, configurate il framework in modo che  Adobe Analytics tenga traccia dei dati dei componenti.

I componenti che interagiscono con il framework Adobe Analytics  vengono visualizzati in SideKick durante la modifica di un framework. Dopo aver trascinato il componente nel framework, vengono visualizzate le proprietà del componente ed è quindi possibile mapparle con  proprietà Adobe Analytics. (Vedere [Impostazione di un framework per il tracciamento di base](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework).)

I componenti possono interagire con il framework Adobe Analytics  quando il componente ha un nodo figlio denominato `analytics`. Il nodo `analytics` ha le seguenti proprietà:

* `cq:trackevents`: Identifica gli eventi CQ esposti dal componente. Consultate Eventi personalizzati.
* `cq:trackvars`: Denomina le variabili CQ mappate con  proprietà Adobe Analytics.
* `cq:componentName`: Nome del componente visualizzato nella barra laterale.
* `cq:componentGroup`: Gruppo nella barra laterale che include il componente.

Il codice nel componente JSP aggiunge il codice javascript alla pagina che attiva il tracciamento e definisce i dati tracciati. Il nome dell&#39;evento e i nomi dei dati utilizzati in javascript devono corrispondere ai valori corrispondenti delle proprietà del nodo `analytics`.

* Utilizzate l&#39;attributo di tracciamento dei dati per tenere traccia dei dati evento al caricamento di una pagina. (Vedere [Tracciamento di eventi personalizzati in fase di caricamento della pagina](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load).)
* Utilizzate la funzione CQ_Analytics.record per tenere traccia dei dati dell&#39;evento quando gli utenti interagiscono con le funzioni della pagina. (Vedere [Tracciamento di eventi personalizzati dopo il caricamento della pagina](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load).)

Quando si utilizzano questi metodi di tracciamento dei dati, il modulo di integrazione Adobe Analytics  esegue automaticamente le chiamate a  Adobe Analytics per registrare gli eventi e i dati.

### Esempio: Tracciamento dei clic di navigazione{#example-tracking-topnav-clicks}

Estende il componente di navigazione iniziale in modo che  Adobe Analytics tenga traccia dei clic sui collegamenti di navigazione nella parte superiore della pagina. Quando si fa clic su un collegamento di navigazione,  Adobe Analytics registra il collegamento su cui è stato fatto clic e la pagina su cui è stato fatto clic.

Le seguenti procedure richiedono che siano già state eseguite le seguenti attività:

* È stata creata un’applicazione CQ.
* È stata creata una  configurazione Adobe Analytics e un  Adobe Analytics Framework.

#### Copiare il componente nav principale {#copy-the-topnav-component}

Copiate il componente nav superiore nell’applicazione CQ. La procedura richiede che l&#39;applicazione sia impostata in CRXDE Lite.

1. Fare clic con il pulsante destro del mouse sul nodo `/libs/foundation/components/topnav` e scegliere Copia.
1. Fare clic con il pulsante destro del mouse sulla cartella Components (Componenti) sotto la cartella dell&#39;applicazione e scegliere Incolla.
1. Fate clic su Salva tutto.

#### Integrazione di topnav con il  Adobe Analytics Framework {#integrating-topnav-with-the-adobe-analytics-framework}

Configurare il componente nav principale e modificare il file JSP per definire gli eventi e i dati di tracciamento.

1. Fare clic con il pulsante destro del mouse sul nodo di navigazione superiore e scegliere Crea > Crea nodo. Specificate i seguenti valori di proprietà e fate clic su OK:

   * Nome: `analytics`
   * Tipo: `nt:unstructured`

1. Aggiungi la seguente proprietà al nodo di analisi per assegnare un nome all’evento di tracciamento:

   * Nome: cq:trackevents
   * Tipo: Stringa
   * Valore: topnavClick

1. Aggiungi la seguente proprietà al nodo Analytics per denominare le variabili di dati:

   * Nome: cq:trackvars
   * Tipo: Stringa
   * Valore: topnavTarget,topnavLocation

1. Aggiungete la seguente proprietà al nodo di analisi per denominare il componente per Barra laterale:

   * Nome: cq:componentName
   * Tipo: Stringa
   * Valore: topnav (tracking)

1. Aggiungi la seguente proprietà al nodo di analisi per denominare il gruppo di componenti per Barra laterale:

   * Nome: cq:componentGroup
   * Tipo: Stringa
   * Valore: Generale

1. Fate clic su Salva tutto.
1. Aprire il file `topnav.jsp`.
1. In un elemento, aggiungete il seguente attributo:

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. Nella parte inferiore della pagina, aggiungete il seguente codice javascript:

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. Fate clic su Salva tutto.

Il contenuto del file `topnav.jsp` deve essere visualizzato come segue:

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG, ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>È spesso consigliabile tenere traccia dei dati da ContextHub. Per informazioni sull&#39;utilizzo di javascript per ottenere queste informazioni, vedere [Accesso ai valori in ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).

#### Aggiunta del componente di tracciamento alla barra laterale {#adding-the-tracking-component-to-sidekick}

Aggiungete componenti abilitati per il tracciamento con la barra laterale  Adobe Analytics per poterli aggiungere al framework.

1. Aprite il framework Adobe Analytics  dalla configurazione Adobe Analytics . ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. Nella barra laterale fate clic sul pulsante Progettazione.

   ![](assets/chlimage_1a.png)

1. Nell’area Configurazione tracciamento collegamenti, fate clic su Configura ereditarietà.

   ![chlimage_1](assets/chlimage_1aa.png)

1. Nell’elenco Componenti consentiti, selezionare la navigazione superiore (tracciamento) nella sezione Generale, quindi fare clic su OK.
1. Espandete la barra laterale per passare alla modalità di modifica. Il componente è ora disponibile nel gruppo Generale.

#### Aggiunta del componente nav principale al framework {#adding-the-topnav-component-to-your-framework}

Trascinate il componente di navigazione superiore nel framework Adobe Analytics  e mappate le variabili ed eventi del componente su  variabili ed eventi Adobe Analytics. (Vedere [Impostazione di un framework per il tracciamento di base](/help/sites-administering/adobeanalytics-connect.md).)

![chlimage_1-1](assets/chlimage_1-1a.png)

Il componente nav principale ora è integrato con il framework Adobe Analytics . Quando aggiungete il componente a una pagina, facendo clic sugli elementi nella barra di navigazione superiore i dati di tracciamento vengono inviati a  Adobe Analytics.

### Invio di dati s.products a  Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

I componenti possono generare dati per la variabile s.products che viene inviata a  Adobe Analytics. Progettate i componenti per contribuire alla variabile s.products:

* Registra un valore denominato `product` di una struttura specifica.
* Esporre i membri di dati del valore `product` in modo che possano essere mappati con  variabili Adobe Analytics nel framework Adobe Analytics .

La variabile Adobe Analytics s.products  utilizza la sintassi seguente:

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

Il modulo di integrazione  Adobe Analytics crea la variabile `s.products` utilizzando i valori `product` generati AEM componenti. Il valore `product` in javascript generato AEM componenti è un array di valori con la struttura seguente:

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

Quando un elemento dati viene omesso dal valore `product`, viene inviato come una stringa vuota in s.products.

>[!NOTE]
>
>Quando nessun evento è associato a un valore di prodotto,  Adobe Analytics utilizza l&#39;evento `prodView` per impostazione predefinita.

Il nodo `analytics` del componente deve esporre i nomi delle variabili utilizzando la proprietà `cq:trackvars`:

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

Il modulo eCommerce fornisce diversi componenti che generano dati variabili s.products. Ad esempio, il componente per l&#39;ordine di invio ([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp)) genera un codice JavaScript simile al seguente esempio:

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### Limitazione delle dimensioni delle chiamate di tracciamento {#limiting-the-size-of-tracking-calls}

In genere, i browser Web limitano la dimensione delle richieste di GET. Poiché i valori di prodotto CQ e SKU sono percorsi di repository, gli array di prodotti che includono più valori possono superare il limite di dimensione della richiesta. Pertanto, i componenti devono limitare il numero di elementi nell&#39;array `product` di ogni `CQ_Analytics.record function`. Create più funzioni se il numero di elementi da monitorare può superare il limite.

Ad esempio, il componente Ordine di invio di eCommerce limita a quattro il numero di elementi `product` in una chiamata. Quando il carrello contiene più di quattro prodotti, genera più funzioni `CQ_Analytics.record`.
