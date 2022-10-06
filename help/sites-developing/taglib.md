---
title: Librerie di tag
seo-title: Tag Libraries
description: Le librerie di tag Granite, CQ e Sling consentono di accedere a funzioni specifiche da utilizzare nello script JSP dei modelli e dei componenti
seo-description: The Granite, CQ, and Sling tag libraries give you access to specific functions for use in the JSP script of your templates and components
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
source-git-commit: de5eb53f6160991ca0718d61afaeed2078a4fa88
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 1%

---

# Librerie di tag{#tag-libraries}

Le librerie di tag Granite, CQ e Sling consentono di accedere a funzioni specifiche da utilizzare nello script JSP dei modelli e dei componenti.

## Libreria di tag Granite {#granite-tag-library}

La libreria di tag Granite contiene funzioni utili.

Quando si sviluppa lo script jsp di un componente dell’interfaccia utente Granite, si consiglia di includere il seguente codice nella parte superiore dello script:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

Il globale dichiara anche il [Libreria Sling](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

La `<ui:includeClientLib>` tag Include una libreria client HTML AEM, che può essere un js, un css o una libreria di temi. Per più inclusioni di tipi diversi, ad esempio js e css, questo tag deve essere utilizzato più volte nel jsp. Questo tag è un wrapper per la convenienza ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` interfaccia del servizio.

Ha i seguenti attributi:

**categorie** - Elenco di categorie di libreria client separate da virgola. Questo includerà tutte le librerie JavaScript e CSS per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema** - Elenco di categorie di libreria client separate da virgola. Questo includerà tutte le librerie correlate al tema (sia CSS che JS) per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** - Elenco di categorie di libreria client separate da virgola. Questo includerà tutte le librerie JavaScript per le categorie specificate.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** - Elenco di categorie di libreria client separate da virgola. Questo includerà tutte le librerie CSS per le categorie specificate.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**a tema** - È necessario includere un flag che indica solo le librerie a tema o non a tema. Se omesso, verranno inclusi entrambi i set. Si applica solo a JS o agli include CSS puri (non per le categorie o i temi inclusi).

La `<ui:includeClientLib>` Il tag può essere utilizzato come segue in un jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## Libreria di tag CQ {#cq-tag-library}

La libreria dei tag CQ contiene funzioni utili.

Per utilizzare la libreria di tag CQ nel tuo script, lo script deve iniziare con il seguente codice:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Quando il `/libs/foundation/global.jsp` file incluso nello script, taglib viene dichiarato automaticamente.

Quando si sviluppa lo script jsp di un componente AEM, si consiglia di includere il seguente codice nella parte superiore dello script:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Dichiara i tag sling, CQ e jstl ed espone gli oggetti di script utilizzati regolarmente definiti da [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects) tag . Questo accorcia e semplifica il codice jsp del tuo componente.

### &lt;cq:text> {#cq-text}

La `<cq:text>` tag è un tag di convenienza che produce il testo di un componente in un JSP.

Dispone dei seguenti attributi facoltativi:

**property** - Nome della proprietà da utilizzare. Il nome è relativo alla risorsa corrente.

**value** - Valore da utilizzare per l&#39;output. Se questo attributo è presente, sovrascrive l&#39;utilizzo dell&#39;attributo di proprietà.

**oldValue** - Valore da utilizzare per l&#39;output delle differenze. Se questo attributo è presente, sovrascrive l&#39;utilizzo dell&#39;attributo di proprietà.

**escapeXml** - Definisce se i caratteri &lt;, >, &amp;, &quot; e &quot; nella stringa risultante devono essere convertiti nei corrispondenti codici di entità caratteri. Il valore predefinito è false. L&#39;escape viene applicato dopo la formattazione facoltativa.

**format** - Formato java.text.Format facoltativo da utilizzare per la formattazione del testo.

**noDiff** - Sopprime il calcolo di un output di diff, anche se è presente un&#39;informazione di diff.

**tagClass** - Nome della classe CSS di un elemento che racchiude un output non vuoto. Se vuoto, non viene aggiunto alcun elemento.

**tagName** - Nome dell&#39;elemento che racchiude un output non vuoto. Viene impostato automaticamente su DIV.

**segnaposto** - Valore predefinito da utilizzare per il testo nullo o vuoto in modalità di modifica, ovvero il segnaposto. Il controllo predefinito viene eseguito dopo la formattazione facoltativa e l&#39;escape, ovvero viene scritto così come è nell&#39;output. Per impostazione predefinita:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default** - Valore predefinito da utilizzare per il testo nullo o vuoto. Il controllo predefinito viene eseguito dopo la formattazione facoltativa e l&#39;escape, ovvero viene scritto così come è nell&#39;output.

Alcuni esempi mostrano come `<cq:text>` può essere utilizzato in un JSP:

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### &lt;cq:setContentBundle> {#cq-setcontentbundle}

La `<cq:setContentBundle>` crea un contesto di localizzazione i18n e lo memorizza nel `javax.servlet.jsp.jstl.fmt.localizationContext` variabile di configurazione.

Ha i seguenti attributi:

**language** - La lingua delle impostazioni internazionali per la quale recuperare il bundle di risorse.

**source** - L&#39;origine da cui devono essere prelevate le impostazioni internazionali. Può essere impostato su uno dei seguenti valori:

* **statico** - le impostazioni internazionali vengono prese dal `language` se disponibile, altrimenti dalle impostazioni internazionali predefinite del server.

* **page** - le impostazioni internazionali vengono prese dalla lingua della pagina o della risorsa corrente, se disponibile, in caso contrario dal `language` se disponibile, altrimenti dalle impostazioni internazionali predefinite del server.

* **richiesta** - le impostazioni internazionali vengono prese dalle impostazioni internazionali della richiesta ( `request.getLocale()`).

* **auto** - le impostazioni internazionali vengono prese dal `language` se disponibile, in caso contrario dalla lingua della pagina o della risorsa corrente, se disponibile, altrimenti dalla richiesta.

Se la `source` attributo non impostato:

* Se la `language` è impostato l&#39;attributo `source` attributo predefinito in &quot; `static`.

* Se la `language` attributo non impostato, il `source` impostazioni predefinite attributo `auto`.

Il &quot;pacchetto di contenuti&quot; può essere utilizzato semplicemente da JSTL standard `<fmt:message>` tag. La ricerca dei messaggi tramite chiavi è duplice:

1. Innanzitutto, per cercare le traduzioni, cerca le proprietà JCR della risorsa sottostante di cui è attualmente eseguito il rendering. Questo consente di definire una semplice finestra di dialogo del componente per modificare tali valori.
1. Se il nodo non contiene una proprietà denominata esattamente come la chiave, il fallback consiste nel caricare un bundle di risorse dalla richiesta sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). La lingua o le impostazioni internazionali di questo bundle sono definite dagli attributi di lingua e origine del `<cq:setContentBundle>` tag .

La `<cq:setContentBundle>` Il tag può essere utilizzato come segue in un jsp.

Per le pagine che ne definiscono la lingua:

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

Per pagine personalizzate dall’utente:

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

La `<cq:include>` Il tag include una risorsa nella pagina corrente.

Ha i seguenti attributi:

**scaricatore**

* Valore booleano che definisce se eseguire il flush dell’output prima di includere la destinazione.

**path**

* Percorso dell&#39;oggetto risorsa da includere nell&#39;elaborazione della richiesta corrente. Se il percorso è relativo, viene aggiunto al percorso della risorsa corrente il cui script include la risorsa specificata. È necessario specificare percorso e resourceType o script.

**resourceType**

* Tipo di risorsa della risorsa da includere. Se è impostato il tipo di risorsa, il percorso deve corrispondere esattamente al percorso di un oggetto risorsa: in questo caso, l&#39;aggiunta di parametri, selettori ed estensioni al percorso non è supportata.
* Se la risorsa da includere è specificata con l’attributo percorso che non può essere risolto in una risorsa, il tag può creare un oggetto risorsa sintetico fuori dal percorso e da questo tipo di risorsa.
* È necessario specificare percorso e resourceType o script.

**script**

* Lo script jsp da includere. È necessario specificare percorso e resourceType o script.

**ignoreComponentHierarchy**

* Valore booleano che controlla se la gerarchia dei componenti deve essere ignorata per la risoluzione degli script. Se true, vengono rispettati solo i percorsi di ricerca.

**Esempio:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

Utilizza `<%@ include file="myScript.jsp" %>` o `<cq:include script="myScript.jsp" %>` per includere uno script?

* La `<%@ include file="myScript.jsp" %>` La direttiva informa il compilatore JSP di includere un file completo nel file corrente. È come se il contenuto del file incluso fosse stato incollato direttamente nel file originale.
* Con la `<cq:include script="myScript.jsp">` Il file viene incluso in fase di runtime.

Utilizza `<cq:include>` o `<sling:include>`?

* Durante lo sviluppo di componenti AEM, l’Adobe consiglia di utilizzare `<cq:include>`.
* `<cq:include>` consente di includere direttamente i file di script in base al loro nome quando si utilizza l’attributo script. Questo prende in considerazione l’ereditarietà di componenti e tipi di risorse ed è spesso più semplice della rigorosa aderenza alla risoluzione degli script di Sling utilizzando selettori ed estensioni.

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` è stato dichiarato obsoleto a partire dal AEM 5.6. [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) Deve essere invece utilizzato.

La `<cq:includeClientLib>` tag Include una libreria client HTML AEM, che può essere un js, un css o una libreria di temi. Per più inclusioni di tipi diversi, ad esempio js e css, questo tag deve essere utilizzato più volte nel jsp. Questo tag è un wrapper per la convenienza `com.day.cq.widget.HtmlLibraryManager` interfaccia del servizio.

Ha i seguenti attributi:

**categorie** - Elenco di categorie di libreria client separate da virgola. Questo includerà tutte le librerie JavaScript e CSS per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema** - Elenco di categorie di libreria client separate da virgola. Questo includerà tutte le librerie correlate al tema (sia CSS che JS) per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js** - Elenco di categorie di libreria client separate da virgola. Questo includerà tutte le librerie JavaScript per le categorie specificate.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** - Elenco di categorie di libreria client separate da virgola. Questo includerà tutte le librerie CSS per le categorie specificate.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**a tema** - È necessario includere un flag che indica solo le librerie a tema o non a tema. Se omesso, verranno inclusi entrambi i set. Si applica solo a JS o agli include CSS puri (non per le categorie o i temi inclusi).

La `<cq:includeClientLib>` Il tag può essere utilizzato come segue in un jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### &lt;cq:defineObjects> {#cq-defineobjects}

La `<cq:defineObjects>` Il tag espone i seguenti oggetti di script, utilizzati regolarmente e a cui lo sviluppatore può fare riferimento. Inoltre espone gli oggetti definiti dal [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects) tag .

**componentContext**

* l’oggetto contestuale del componente corrente della richiesta (com.day.cq.wcm.api.components.ComponentContext interface).

**componente**

* l’oggetto componente AEM corrente della risorsa corrente (com.day.cq.wcm.api.components.Component interface).

**currentDesign**

* l&#39;oggetto struttura corrente della pagina corrente (interfaccia com.day.cq.wcm.api.designer.Design).

**currentPage**

* l’oggetto pagina WCM AEM corrente (interfaccia com.day.cq.wcm.api.Page).

**currentStyle**

* l&#39;oggetto stile corrente della cella corrente (interfaccia com.day.cq.wcm.api.designer.Style).

**designer**

* l’oggetto designer utilizzato per accedere alle informazioni di progettazione (interfaccia com.day.cq.wcm.api.designer.Designer).

**editContext**

* l’oggetto edit context del componente AEM (com.day.cq.wcm.api.components.EditContext interface).

**pageManager**

* l’oggetto page manager per le operazioni a livello di pagina (interfaccia com.day.cq.wcm.api.PageManager).

**pageProperties**

* l&#39;oggetto page properties della pagina corrente (org.apache.sling.api.resource.ValueMap).

**proprietà**

* l&#39;oggetto properties della risorsa corrente (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* l’oggetto design della pagina delle risorse (interfaccia com.day.cq.wcm.api.designer.Design).

**resourcePage**

* l’oggetto page della risorsa (com.day.cq.wcm.api.Page interface).
* Ha i seguenti attributi:

**requestName**

* ereditato da sling

**responseName**

* ereditato da sling

**resourceName**

* ereditato da sling

**nodeName**

* ereditato da sling

**logName**

* ereditato da sling

**resourceResolverName**

* ereditato da sling

**slingName**

* ereditato da sling

**componentContextName**

* specifico per wcm

**editContextName**

* specifico per wcm

**propertiesName**

* specifico per wcm

**pageManagerName**

* specifico per wcm

**currentPageName**

* specifico per wcm

**resourcePageName**

* specifico per wcm

**pagePropertiesName**

* specifico per wcm

**componentName**

* specifico per wcm

**designerName**

* specifico per wcm

**currentDesignName**

* specifico per wcm

**resourceDesignName**

* specifico per wcm

**currentStyleName**

* specifico per wcm

**Esempio**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>Quando il `/libs/foundation/global.jsp` è incluso nello script, il `<cq:defineObjects />` viene incluso automaticamente.

### &lt;cq:requestURL> {#cq-requesturl}

La `<cq:requestURL>` scrive l&#39;URL della richiesta corrente in JspWriter. I due tag [ `<cq:addParam>`](#amp-lt-cq-addparam) e [ `<cq:removeParam>`](#amp-lt-cq-removeparam) e può essere utilizzato all’interno del corpo di questo tag per modificare l’URL della richiesta corrente prima che venga scritto.

Consente di creare collegamenti alla pagina corrente con parametri variabili. Ad esempio, ti consente di trasformare la richiesta:

`mypage.html?mode=view&query=something` in `mypage.html?query=something`.

L&#39;uso di `addParam` o `removeParam` cambia solo l&#39;occorrenza del parametro dato, tutti gli altri parametri non vengono modificati.

`<cq:requestURL>` non ha alcun attributo.

Esempi:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

La `<cq:addParam>` aggiunge un parametro di richiesta con il nome e il valore specificati all’allegato [ `<cq:requestURL>`](#amp-lt-cq-requesturl) tag .

Ha i seguenti attributi:

**name**

* nome del parametro da aggiungere

**valore**

* valore del parametro da aggiungere

**Esempio:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

La `<cq:removeParam>` rimuove un parametro di richiesta con il nome e il valore specificati dall’allegato [ `<cq:requestURL>`](#amp-lt-cq-requesturl) tag . Se non viene fornito alcun valore, vengono rimossi tutti i parametri con il nome specificato.

Ha i seguenti attributi:

**name**

* nome del parametro da rimuovere

Esempio:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Libreria di tag Sling {#sling-tag-library}

La libreria di tag Sling contiene utili funzioni Sling.

Quando utilizzi la libreria di tag Sling nello script, lo script deve iniziare con il seguente codice:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Quando il `/libs/foundation/global.jsp` file incluso nello script, il tag sling viene dichiarato automaticamente.

### &lt;sling:include> {#sling-include}

La `<sling:include>` Il tag include una risorsa nella pagina corrente.

Ha i seguenti attributi:

**scaricatore**

* Valore booleano che definisce se eseguire il flush dell’output prima di includere la destinazione.

**resource**

* L&#39;oggetto risorsa da includere nell&#39;elaborazione della richiesta corrente. Specificare la risorsa o il percorso. Se vengono specificati entrambi, la risorsa ha la precedenza.

**path**

* Percorso dell&#39;oggetto risorsa da includere nell&#39;elaborazione della richiesta corrente. Se il percorso è relativo, viene aggiunto al percorso della risorsa corrente il cui script include la risorsa specificata. Specificare la risorsa o il percorso. Se vengono specificati entrambi, la risorsa ha la precedenza.

**resourceType**

* Tipo di risorsa della risorsa da includere. Se è impostato il tipo di risorsa, il percorso deve corrispondere esattamente al percorso di un oggetto risorsa: in questo caso, l&#39;aggiunta di parametri, selettori ed estensioni al percorso non è supportata.
* Se la risorsa da includere è specificata con l’attributo percorso che non può essere risolto in una risorsa, il tag può creare un oggetto risorsa sintetico fuori dal percorso e da questo tipo di risorsa.

**replaceSelectors**

* Durante l’invio, i selettori vengono sostituiti con il valore di questo attributo.

**addSelectors**

* Durante l’invio, il valore di questo attributo viene aggiunto ai selettori.

**replaceSuffix**

* Durante l&#39;invio, il suffisso viene sostituito dal valore di questo attributo.

>[!NOTE]
>
>La risoluzione della risorsa e dello script incluso nella `<sling:include>` è lo stesso di una normale risoluzione URL sling. Per impostazione predefinita, i selettori, l’estensione, ecc. dalla richiesta corrente vengono utilizzati anche per lo script incluso. Possono essere modificati tramite gli attributi del tag: per esempio `replaceSelectors="foo.bar"` consente di sovrascrivere i selettori.

Esempi:

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### &lt;sling:defineObjects> {#sling-defineobjects}

La `<sling:defineObjects>` Il tag espone i seguenti oggetti di script, utilizzati regolarmente e a cui lo sviluppatore può fare riferimento:

**slingRequest**

* L&#39;oggetto SlingHttpServletRequest, fornendo l&#39;accesso alle informazioni di intestazione della richiesta HTTP - estende la richiesta standard HttpServletRequest - e fornisce l&#39;accesso a elementi specifici di Sling come risorsa, informazioni sul percorso, selettore, ecc.

**slingResponse**

* Oggetto SlingHttpServletResponse, che fornisce l&#39;accesso per la risposta HTTP creata dal server. Attualmente è lo stesso di HttpServletResponse da cui si estende.**richiesta**
* L&#39;oggetto di richiesta JSP standard che è un HttpServletRequest puro.**response**
* L&#39;oggetto di risposta JSP standard che è una risposta HttpServletResponse pura.

**resourceResolver**

* L&#39;oggetto ResourceResolver corrente. È lo stesso di slingRequest.getResourceResolver()

.**sling**

* Un oggetto SlingScriptHelper contenente metodi di convenienza per gli script, principalmente sling.include(&#39;/some/other/resource&#39;) per includere le risposte di altre risorse all&#39;interno di questa risposta (ad esempio incorporamento di snippet html di intestazione) e sling.getService(foo.bar.Service.class) per recuperare i servizi OSGi disponibili in Sling (Notazione classe a seconda del linguaggio di script).

**risorsa**

* l&#39;oggetto Resource corrente da gestire, a seconda dell&#39;URL della richiesta. È lo stesso di slingRequest.getResource().

**currentNode**

* Se la risorsa corrente punta a un nodo JCR (che in genere è il caso in Sling), questo dà accesso diretto all&#39;oggetto Node. In caso contrario, questo oggetto non è definito.

**log**

* Fornisce un logger SLF4J per la registrazione nel sistema di log Sling dall&#39;interno di script, ad esempio log.info(&quot;Esecuzione dello script&quot;).

* Ha i seguenti attributi:

**requestName**

**responseName**

**nodeName**

l **ogName resourceResolverName**

**slingName**

**Esempio:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## Libreria di tag JSTL {#jstl-tag-library}

La [Libreria di tag standard delle pagine JavaServer](https://www.oracle.com/technetwork/java/index-jsp-135995.html) contiene molti tag utili e standard. Le librerie di base, di formattazione e di funzioni sono definite dal `/libs/foundation/global.jsp` come mostrato nel frammento seguente.

### Estratto di /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Dopo l’importazione della `/libs/foundation/global.jsp` come descritto in precedenza, è possibile utilizzare `c`, `fmt` e `fn` prefissi per accedere a tali tag libs. La documentazione ufficiale della JSTL è disponibile all&#39;indirizzo [Tutorial su Java EE 5 - Libreria di tag standard delle pagine JavaServer](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
