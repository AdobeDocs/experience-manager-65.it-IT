---
title: Librerie di tag
seo-title: Librerie di tag
description: Le librerie di tag Granite, CQ e Sling consentono di accedere a funzioni specifiche da utilizzare nello script JSP dei modelli e dei componenti
seo-description: Le librerie di tag Granite, CQ e Sling consentono di accedere a funzioni specifiche da utilizzare nello script JSP dei modelli e dei componenti
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 1%

---


# Librerie di tag{#tag-libraries}

Le librerie di tag Granite, CQ e Sling consentono di accedere a funzioni specifiche da utilizzare nello script JSP dei modelli e dei componenti.

## Libreria di tag Granite {#granite-tag-library}

La libreria di tag Granite contiene funzioni utili.

Quando si sviluppa lo script jsp di un componente dell&#39;interfaccia utente Granite, è consigliabile includere il seguente codice nella parte superiore dello script:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

Il globale dichiara inoltre la [libreria Sling](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### <ui:includeClientLib> {#ui-includeclientlib}

Il tag `<ui:includeClientLib>` include una libreria client HTML AEM, che può essere un js, un css o una libreria di temi. Per più inclusioni di tipi diversi, ad esempio js e css, questo tag deve essere utilizzato più volte nel jsp. Questo tag è un wrapper per comodità intorno all&#39;interfaccia del servizio ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)`.

Ha i seguenti attributi:

**categorie**  - Un elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie Javascript e CSS per le categorie indicate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema**  - Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie correlate ai temi (sia CSS che JS) per le categorie indicate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js**  - Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie Javascript per le categorie indicate.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css**  - Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie CSS per le categorie specificate.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**temed** - È necessario includere un flag che indica solo le librerie a tema o non a tema. Se omesso, entrambi i set saranno inclusi. Applicabile solo a JS o CSS puri (non per le categorie o i temi inclusi).

Il tag `<ui:includeClientLib>` può essere utilizzato come segue in un jsp:

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

La libreria di tag CQ contiene funzioni utili.

Per utilizzare la libreria di tag CQ nello script, lo script deve iniziare con il seguente codice:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Quando il file `/libs/foundation/global.jsp` è incluso nello script, il tag lib viene dichiarato automaticamente.

Quando si sviluppa lo script jsp di un componente AEM, si consiglia di includere il seguente codice nella parte superiore dello script:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Dichiara gli tag sling, CQ e jstl ed espone gli oggetti di script utilizzati regolarmente definiti dal tag [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects). Questo accorcia e semplifica il codice jsp del componente.

### <cq:text> {#cq-text}

Il tag `<cq:text>` è un tag di convenienza che produce il testo di un componente in un JSP.

Contiene i seguenti attributi facoltativi:

**property** - Nome della proprietà da utilizzare. Il nome è relativo alla risorsa corrente.

**value** - Valore da utilizzare per l&#39;output. Se questo attributo è presente, sovrascrive l&#39;uso dell&#39;attributo property.

**oldValue** - Valore da utilizzare per l&#39;output delle diff. Se questo attributo è presente, sovrascrive l&#39;uso dell&#39;attributo property.

**escapeXml**  - Definisce se i caratteri  &lt;>, &amp;, &#39; e &quot; nella stringa risultante devono essere convertiti nei codici di entità carattere corrispondenti. Il valore predefinito è false. L&#39;escape viene applicato dopo la formattazione facoltativa.

**format** - Facoltativo java.text.Format per formattare il testo.

**noDiff**  - Elimina il calcolo di un output diff, anche se sono presenti informazioni diff.

**tagClass** - Nome classe CSS di un elemento che racchiude un output non vuoto. Se vuoto, non viene aggiunto alcun elemento.

**tagName** - Nome dell&#39;elemento che racchiude un output non vuoto. Il valore predefinito è DIV.

**segnaposto**  - Valore predefinito da utilizzare per testo nullo o vuoto in modalità di modifica, ad esempio il segnaposto. Il controllo predefinito viene eseguito dopo la formattazione facoltativa e l&#39;escape, ovvero viene scritto così come è nell&#39;output. Per impostazione predefinita:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default**  - Valore predefinito da utilizzare per il testo nullo o vuoto. Il controllo predefinito viene eseguito dopo la formattazione facoltativa e l&#39;escape, ovvero viene scritto così come è nell&#39;output.

Alcuni esempi di utilizzo del tag `<cq:text>` in un JSP:

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

### <cq:setContentBundle> {#cq-setcontentbundle}

Il tag `<cq:setContentBundle>` crea un contesto di localizzazione i18n e lo memorizza nella variabile di configurazione `javax.servlet.jsp.jstl.fmt.localizationContext`.

Ha i seguenti attributi:

**lingua**  - La lingua delle impostazioni internazionali per cui recuperare il bundle di risorse.

**source**  - L&#39;origine da cui devono essere utilizzate le impostazioni internazionali. Può essere impostato su uno dei seguenti valori:

* **static** : le impostazioni internazionali sono estratte dall&#39; `language` attributo, se disponibile, altrimenti dalle impostazioni internazionali predefinite del server.

* **page** - le impostazioni internazionali sono estratte dalla lingua della pagina o della risorsa corrente, se disponibile, altrimenti dall&#39; `language` attributo, se disponibile, altrimenti dalle impostazioni internazionali predefinite del server.

* **request** - le impostazioni internazionali vengono estratte dalle impostazioni internazionali della richiesta (  `request.getLocale()`).

* **auto**  - le impostazioni internazionali sono estratte dall&#39; `language` attributo, se disponibile, altrimenti dalla lingua della pagina o risorsa corrente, se disponibile, altrimenti dalla richiesta.

Se l&#39;attributo `source` non è impostato:

* Se l&#39;attributo `language` è impostato, per impostazione predefinita l&#39;attributo `source` è &quot;`static`.

* Se l&#39;attributo `language` non è impostato, per impostazione predefinita l&#39;attributo `source` è `auto`.

Il &quot;pacchetto di contenuti&quot; può essere semplicemente utilizzato dai tag JSTL `<fmt:message>` standard. La ricerca dei messaggi in base alle chiavi è duplice:

1. Innanzitutto, per le proprietà JCR della risorsa sottostante di cui è attualmente eseguito il rendering vengono ricercate le traduzioni. Questo consente di definire una semplice finestra di dialogo dei componenti per modificare tali valori.
1. Se il nodo non contiene una proprietà denominata esattamente come la chiave, l&#39;fallback consiste nel caricare un bundle di risorse dalla richiesta di sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). La lingua o le impostazioni internazionali per questo bundle sono definite dagli attributi di lingua e origine del tag `<cq:setContentBundle>`.

Il tag `<cq:setContentBundle>` può essere utilizzato come segue in un jsp.

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

### <cq:include> {#cq-include}

Il tag `<cq:include>` include una risorsa nella pagina corrente.

Ha i seguenti attributi:

**rossore**

* Valore booleano che definisce se cancellare l&#39;output prima di includere la destinazione.

**path**

* Percorso dell&#39;oggetto risorsa da includere nell&#39;elaborazione della richiesta corrente. Se il percorso è relativo, viene aggiunto al percorso della risorsa corrente il cui script include la risorsa specificata. È necessario specificare percorso e resourceType o script.

**resourceType**

* Il tipo di risorsa della risorsa da includere. Se il tipo di risorsa è impostato, il percorso deve corrispondere esattamente a quello di un oggetto risorsa: in questo caso, l&#39;aggiunta di parametri, selettori ed estensioni al percorso non è supportata.
* Se la risorsa da includere è specificata con l&#39;attributo percorso che non può essere risolto in una risorsa, il tag può creare un oggetto risorsa sintetico al di fuori del percorso e di questo tipo di risorsa.
* È necessario specificare percorso e resourceType o script.

**script**

* Lo script jsp da includere. È necessario specificare percorso e resourceType o script.

**ignoreComponentHierarchy**

* Valore booleano che controlla se la gerarchia dei componenti deve essere ignorata per la risoluzione dello script. Se true, vengono rispettati solo i percorsi di ricerca.

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

Utilizzare `<%@ include file="myScript.jsp" %>` o `<cq:include script="myScript.jsp" %>` per includere uno script?

* La direttiva `<%@ include file="myScript.jsp" %>` informa il compilatore JSP di includere un file completo nel file corrente. È come se i contenuti del file incluso fossero incollati direttamente nel file originale.
* Con il tag `<cq:include script="myScript.jsp">`, il file viene incluso in fase di esecuzione.

Utilizzare `<cq:include>` o `<sling:include>`?

* Durante lo sviluppo AEM componenti,  Adobe consiglia di utilizzare `<cq:include>`.
* `<cq:include>` consente di includere direttamente i file di script in base al nome quando si utilizza l&#39;attributo di script. Questo prende in considerazione l&#39;ereditarietà di componenti e tipi di risorse ed è spesso più semplice rispetto alla rigorosa conformità alla risoluzione dello script di Sling utilizzando selettori ed estensioni.

### <cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` è stato dichiarato obsoleto a partire dal AEM 5.6.  [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) dovrebbe essere utilizzato al posto.

Il tag `<cq:includeClientLib>` include una libreria client HTML AEM, che può essere un js, un css o una libreria di temi. Per più inclusioni di tipi diversi, ad esempio js e css, questo tag deve essere utilizzato più volte nel jsp. Questo tag è un wrapper per comodità intorno all&#39;interfaccia del servizio `com.day.cq.widget.HtmlLibraryManager`.

Ha i seguenti attributi:

**categorie**  - Un elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie Javascript e CSS per le categorie indicate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema**  - Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie correlate ai temi (sia CSS che JS) per le categorie indicate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js**  - Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie Javascript per le categorie indicate.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css**  - Elenco di categorie di lib client separate da virgole. Questo includerà tutte le librerie CSS per le categorie specificate.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**temed** - È necessario includere un flag che indica solo le librerie a tema o non a tema. Se omesso, entrambi i set saranno inclusi. Applicabile solo a JS o CSS puri (non per le categorie o i temi inclusi).

Il tag `<cq:includeClientLib>` può essere utilizzato come segue in un jsp:

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

### <cq:defineObjects> {#cq-defineobjects}

Il tag `<cq:defineObjects>` espone i seguenti oggetti di script, utilizzati regolarmente, ai quali lo sviluppatore può fare riferimento. Inoltre, espone gli oggetti definiti dal tag [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects).

**componentContext**

* l’oggetto contestuale del componente corrente della richiesta (com.day.cq.wcm.api.components.ComponentContext interface).

**componente**

* l’oggetto componente AEM corrente della risorsa corrente (interfaccia com.day.cq.wcm.api.components.Component).

**currentDesign**

* l&#39;oggetto di progettazione corrente della pagina corrente (interfaccia com.day.cq.wcm.api.designer.Design).

**currentPage**

* l&#39;oggetto pagina WCM AEM corrente (interfaccia com.day.cq.wcm.api.Page).

**currentStyle**

* l&#39;oggetto stile corrente della cella corrente (interfaccia com.day.cq.wcm.api.designer.Style).

**designer**

* l&#39;oggetto designer utilizzato per accedere alle informazioni di progettazione (interfaccia com.day.cq.wcm.api.designer.Designer).

**editContext**

* l’oggetto contesto di modifica del componente AEM (interfaccia com.day.cq.wcm.api.components.EditContext).

**pageManager**

* l&#39;oggetto page manager per le operazioni a livello di pagina (interfaccia com.day.cq.wcm.api.PageManager).

**pageProperties**

* l’oggetto delle proprietà della pagina corrente (org.apache.sling.api.resource.ValueMap).

**proprietà**

* l&#39;oggetto properties della risorsa corrente (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* l&#39;oggetto di progettazione della pagina delle risorse (interfaccia com.day.cq.wcm.api.designer.Design).

**resourcePage**

* l&#39;oggetto pagina delle risorse (interfaccia com.day.cq.wcm.api.Page).
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

* specifica per wcm

**editContextName**

* specifica per wcm

**propertiesName**

* specifica per wcm

**pageManagerName**

* specifica per wcm

**currentPageName**

* specifica per wcm

**resourcePageName**

* specifica per wcm

**pagePropertiesName**

* specifica per wcm

**componentName**

* specifica per wcm

**designerName**

* specifica per wcm

**currentDesignName**

* specifica per wcm

**resourceDesignName**

* specifica per wcm

**currentStyleName**

* specifica per wcm

**Esempio**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>Quando il file `/libs/foundation/global.jsp` è incluso nello script, il tag `<cq:defineObjects />` viene incluso automaticamente.

### <cq:requestURL> {#cq-requesturl}

Il tag `<cq:requestURL>` scrive l&#39;URL della richiesta corrente in JspWriter. I due tag [ `<cq:addParam>`](#amp-lt-cq-addparam) e [ `<cq:removeParam>`](#amp-lt-cq-removeparam) &lt;a3/> possono essere utilizzati all&#39;interno del corpo di questo tag per modificare l&#39;URL della richiesta corrente prima che venga scritto.

Consente di creare collegamenti alla pagina corrente con parametri variabili. Ad esempio, consente di trasformare la richiesta:

`mypage.html?mode=view&query=something` in `mypage.html?query=something`.

L&#39;utilizzo di `addParam` o `removeParam` modifica solo l&#39;occorrenza del parametro specificato, tutti gli altri parametri non vengono modificati.

`<cq:requestURL>` non ha alcun attributo.

Esempi:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:addParam> {#cq-addparam}

Il tag `<cq:addParam>` aggiunge un parametro di richiesta con il nome e il valore specificati al tag [ `<cq:requestURL>`](#amp-lt-cq-requesturl) che lo contiene.

Ha i seguenti attributi:

**name**

* nome del parametro da aggiungere

**valore**

* valore del parametro da aggiungere

**Esempio:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:removeParam> {#cq-removeparam}

Il tag `<cq:removeParam>` rimuove un parametro di richiesta con il nome e il valore specificati dal tag [ `<cq:requestURL>`](#amp-lt-cq-requesturl) che lo contiene. Se non viene fornito alcun valore, vengono rimossi tutti i parametri con il nome specificato.

Ha i seguenti attributi:

**name**

* nome del parametro da rimuovere

Esempio:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Libreria di tag Sling {#sling-tag-library}

La libreria di tag Sling contiene utili funzioni Sling.

Quando si utilizza la libreria di tag Sling nello script, lo script deve iniziare con il seguente codice:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Quando il file `/libs/foundation/global.jsp` è incluso nello script, il tag sling viene dichiarato automaticamente.

### <sling:include> {#sling-include}

Il tag `<sling:include>` include una risorsa nella pagina corrente.

Ha i seguenti attributi:

**rossore**

* Valore booleano che definisce se cancellare l&#39;output prima di includere la destinazione.

**riferimento**

* L&#39;oggetto risorsa da includere nell&#39;elaborazione della richiesta corrente. È necessario specificare una risorsa o un percorso. Se vengono specificati entrambi, la risorsa ha la precedenza.

**path**

* Percorso dell&#39;oggetto risorsa da includere nell&#39;elaborazione della richiesta corrente. Se il percorso è relativo, viene aggiunto al percorso della risorsa corrente il cui script include la risorsa specificata. È necessario specificare una risorsa o un percorso. Se vengono specificati entrambi, la risorsa ha la precedenza.

**resourceType**

* Il tipo di risorsa della risorsa da includere. Se il tipo di risorsa è impostato, il percorso deve corrispondere esattamente a quello di un oggetto risorsa: in questo caso, l&#39;aggiunta di parametri, selettori ed estensioni al percorso non è supportata.
* Se la risorsa da includere è specificata con l&#39;attributo percorso che non può essere risolto in una risorsa, il tag può creare un oggetto risorsa sintetico al di fuori del percorso e di questo tipo di risorsa.

**replaceSelectors**

* Durante l&#39;invio, i selettori vengono sostituiti con il valore di questo attributo.

**addSelectors**

* Durante l&#39;invio, il valore di questo attributo viene aggiunto ai selettori.

**replaceSuffix**

* Durante l&#39;invio, il suffisso viene sostituito dal valore di questo attributo.

>[!NOTE]
>
>La risoluzione della risorsa e lo script inclusi con il tag `<sling:include>` è uguale a quella di una normale risoluzione URL sling. Per impostazione predefinita, i selettori, le estensioni, ecc. dalla richiesta corrente vengono utilizzati anche per lo script incluso. Possono essere modificati tramite gli attributi del tag: ad esempio `replaceSelectors="foo.bar"` consente di sovrascrivere i selettori.

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

### <sling:defineObjects> {#sling-defineobjects}

Il tag `<sling:defineObjects>` espone i seguenti oggetti di script, utilizzati regolarmente e a cui lo sviluppatore può fare riferimento:

**slingRequest**

* Oggetto SlingHttpServletRequest, che fornisce l&#39;accesso alle informazioni dell&#39;intestazione della richiesta HTTP - estende la richiesta HttpServletRequest standard - e fornisce l&#39;accesso a elementi specifici di Sling come risorsa, informazioni sul percorso, selettore, ecc.

**slingResponse**

* Oggetto SlingHttpServletResponse, che fornisce l&#39;accesso per la risposta HTTP creata dal server. Attualmente è lo stesso di HttpServletResponse da cui si estende.**request**
* L&#39;oggetto di richiesta JSP standard, che è una richiesta HttpServletRequest pura.**response**
* L&#39;oggetto di risposta JSP standard che è un oggetto HttpServletResponse puro.

**resourceResolver**

* L&#39;oggetto ResourceResolver corrente. È lo stesso di slingRequest.getResourceResolver()

.**sling**

* Un oggetto SlingScriptHelper contenente metodi comodi per gli script, principalmente sling.include(&#39;/some/other/resource&#39;) per includere le risposte di altre risorse all&#39;interno di questa risposta (ad esempio per recuperare i servizi OSGi disponibili in Sling (notazione classe a seconda del linguaggio di script) e sling.getService(foo.bar.Service.class).

**riferimento**

* l&#39;oggetto Resource corrente da gestire, in base all&#39;URL della richiesta. È uguale a slingRequest.getResource().

**currentNode**

* Se la risorsa corrente punta a un nodo JCR (che generalmente si verifica in Sling), questo consente l&#39;accesso diretto all&#39;oggetto Node. In caso contrario l&#39;oggetto non è definito.

**log**

* Fornisce un logger SLF4J per l&#39;accesso al sistema di log Sling dall&#39;interno degli script, ad esempio log.info(&quot;Esecuzione dello script&quot;).

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

La [libreria di tag standard delle pagine JavaServer](https://www.oracle.com/technetwork/java/index-jsp-135995.html) contiene molti tag utili e standard. Gli tag core, di formattazione e delle funzioni sono definiti dall&#39; `/libs/foundation/global.jsp` come mostrato nel frammento di codice seguente.

### Estratto di /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Dopo aver importato il file `/libs/foundation/global.jsp` come descritto in precedenza, è possibile utilizzare i prefissi `c`, `fmt` e `fn` per accedere a tali tag. La documentazione ufficiale del JSTL è disponibile all&#39;indirizzo [The Java EE 5 Tutorial - JavaServer Pages Standard Tag Library](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
