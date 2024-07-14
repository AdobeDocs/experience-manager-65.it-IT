---
title: Librerie di tag
description: Le librerie di tag Granite, CQ e Sling consentono di accedere a funzioni specifiche da utilizzare nello script JSP dei modelli e dei componenti
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
solution: Experience Manager, Experience Manager Sites
feature: Developing,Tagging
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2452'
ht-degree: 0%

---

# Librerie di tag{#tag-libraries}

Le librerie di tag Granite, CQ e Sling consentono di accedere a funzioni specifiche da utilizzare nello script JSP dei modelli e dei componenti.

## Libreria tag Granite {#granite-tag-library}

La libreria di tag Granite contiene funzioni utili.

Quando sviluppi lo script jsp di un componente dell’interfaccia utente Granite, si consiglia di includere il seguente codice nella parte superiore dello script:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

La libreria globale dichiara anche la [libreria Sling](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

Il tag `<ui:includeClientLib>` include una libreria client HTML AEM, che può essere una libreria js, css o theme. Per più inclusioni di tipi diversi, ad esempio, js e css, questo tag deve essere utilizzato più volte in jsp. Questo tag è un wrapper di convenienza intorno all&#39;interfaccia del servizio ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)`.

Ha i seguenti attributi:

**categorie** - Elenco di categorie libreria client separate da virgole. Sono incluse tutte le librerie JavaScript e CSS per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema** - Elenco di categorie libreria client separate da virgole. Sono incluse tutte le librerie relative al tema (sia CSS che JS) per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** - Elenco di categorie di librerie client separate da virgole. Sono incluse tutte le librerie JavaScript per le categorie specificate.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** - Elenco di categorie di librerie client separate da virgole. Sono incluse tutte le librerie CSS per le categorie specificate.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**a tema** - Deve essere incluso un flag che indica solo le librerie a tema o non a tema. Se omesso, vengono inclusi entrambi i set. Si applica solo alle inclusioni JS pure o CSS (non per le categorie o i temi).

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

## Libreria tag CQ {#cq-tag-library}

La libreria di tag CQ contiene funzioni utili.

Per utilizzare la libreria di tag CQ nello script, lo script deve iniziare con il seguente codice:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Quando il file `/libs/foundation/global.jsp` è incluso nello script, la taglib viene dichiarata automaticamente.

Quando sviluppi lo script jsp di un componente AEM, si consiglia di includere il seguente codice nella parte superiore dello script:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Dichiara le taglib sling, CQ e jstl ed espone gli oggetti di script utilizzati regolarmente definiti dal tag [`<cq:defineObjects />`](#amp-lt-cq-defineobjects). Questo accorcia e semplifica il codice jsp del componente.

### &lt;cq:text> {#cq-text}

Il tag `<cq:text>` è un tag di convenienza che restituisce il testo di un componente in una JSP.

Sono disponibili i seguenti attributi facoltativi:

**proprietà** - Nome della proprietà da utilizzare. Il nome è relativo alla risorsa corrente.

**valore** - Valore da utilizzare per l&#39;output. Se questo attributo è presente, sovrascrive l&#39;utilizzo dell&#39;attributo property.

**oldValue** - Valore da utilizzare per l&#39;output diff. Se questo attributo è presente, sovrascrive l&#39;utilizzo dell&#39;attributo property.

**escapeXml** - Definisce se i caratteri &lt;, >, &amp;, &#39; e &quot; nella stringa risultante devono essere convertiti nei codici di entità carattere corrispondenti. Il valore predefinito è false. L’escape viene applicato dopo la formattazione facoltativa.

**format** - Java.text.Format facoltativo da utilizzare per la formattazione del testo.

**noDiff** - Elimina il calcolo di un output diff, anche se è presente un&#39;informazione diff.

**tagClass** - Nome di classe CSS di un elemento che racchiuderà un output non vuoto. Se vuoto, non viene aggiunto alcun elemento.

**tagName** - Nome dell&#39;elemento che racchiuderà un output non vuoto. Il valore predefinito è DIV.

**segnaposto** - Valore predefinito da utilizzare per testo nullo o vuoto in modalità di modifica, ovvero il segnaposto. Il controllo predefinito viene eseguito dopo la formattazione facoltativa e l’escape, ovvero viene scritto così com’è nell’output. Il valore predefinito è:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default** - Valore predefinito da utilizzare per testo nullo o vuoto. Il controllo predefinito viene eseguito dopo la formattazione facoltativa e l’escape, ovvero viene scritto così com’è nell’output.

Alcuni esempi di utilizzo del tag `<cq:text>` in una JSP:

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

Il tag `<cq:setContentBundle>` crea un contesto di localizzazione i18n e lo memorizza nella variabile di configurazione `javax.servlet.jsp.jstl.fmt.localizationContext`.

Ha i seguenti attributi:

**lingua**: lingua delle impostazioni locali per cui recuperare il bundle di risorse.

**source** - L&#39;origine da cui prendere le impostazioni locali. Può essere impostato su uno dei seguenti valori:

* **static** - le impostazioni locali vengono ricavate dall&#39;attributo `language`, se disponibile, altrimenti dalle impostazioni locali predefinite del server.

* **pagina** - le impostazioni locali vengono prese dalla lingua della pagina o della risorsa corrente, se disponibile, altrimenti dall&#39;attributo `language` se disponibile, altrimenti dalle impostazioni locali predefinite del server.

* **richiesta** - le impostazioni locali vengono ricavate dalle impostazioni locali della richiesta ( `request.getLocale()`).

* **auto** - le impostazioni locali vengono ricavate dall&#39;attributo `language` se disponibile, altrimenti dalla lingua della pagina o della risorsa corrente se disponibile, altrimenti dalla richiesta.

Se l&#39;attributo `source` non è impostato:

* Se l&#39;attributo `language` è impostato, l&#39;impostazione predefinita dell&#39;attributo `source` è &quot;`static`.

* Se l&#39;attributo `language` non è impostato, per impostazione predefinita l&#39;attributo `source` sarà `auto`.

Il &quot;bundle di contenuti&quot; può essere utilizzato da tag JSTL `<fmt:message>` standard. La ricerca di messaggi tramite chiavi è duplice:

1. Innanzitutto, cerca le traduzioni per le proprietà JCR della risorsa sottostante di cui viene eseguito il rendering. In questo modo è possibile definire una finestra di dialogo per la modifica di tali valori.
1. Se il nodo non contiene una proprietà denominata esattamente come la chiave, il fallback consiste nel caricare un bundle di risorse dalla richiesta sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). La lingua o le impostazioni locali per questo bundle sono definite dagli attributi di lingua e origine del tag `<cq:setContentBundle>`.

Il tag `<cq:setContentBundle>` può essere utilizzato come segue in un jsp.

Per le pagine che definiscono la lingua:

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

Per le pagine personalizzate dall’utente:

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

Il tag `<cq:include>` include una risorsa nella pagina corrente.

Ha i seguenti attributi:

**scarica**

* Valore booleano che definisce se eseguire il flushing dell’output prima di includere la destinazione.

**percorso**

* Percorso dell’oggetto risorsa da includere nell’elaborazione della richiesta corrente. Se il percorso è relativo, viene aggiunto al percorso della risorsa corrente il cui script include la risorsa specificata. È necessario specificare path e resourceType o script.

**tiporisorsa**

* Tipo di risorsa della risorsa da includere. Se il tipo di risorsa è impostato, il percorso deve essere il percorso esatto di un oggetto risorsa: in questo caso, l’aggiunta di parametri, selettori ed estensioni al percorso non è supportata.
* Se la risorsa da includere è specificata con l’attributo path che non può essere risolto in una risorsa, il tag può creare un oggetto risorsa sintetico fuori dal percorso e da questo tipo di risorsa.
* È necessario specificare path e resourceType o script.

**script**

* Lo script JSP da includere. È necessario specificare path e resourceType o script.

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

* La direttiva `<%@ include file="myScript.jsp" %>` informa il compilatore JSP di includere un file completo nel file corrente. È come se il contenuto del file incluso fosse incollato direttamente nel file originale.
* Con il tag `<cq:include script="myScript.jsp">`, il file viene incluso in fase di esecuzione.

Utilizzare `<cq:include>` o `<sling:include>`?

* Durante lo sviluppo di componenti AEM, Adobe consiglia di utilizzare `<cq:include>`.
* `<cq:include>` consente di includere direttamente i file script in base al nome quando si utilizza l&#39;attributo script. Questo prende in considerazione l’ereditarietà del componente e del tipo di risorsa ed è spesso più semplice che una stretta aderenza alla risoluzione dello script di Sling utilizzando selettori ed estensioni.

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` obsoleto da AEM 5.6. Utilizzare [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib).

Il tag `<cq:includeClientLib>` include una libreria client HTML AEM, che può essere una libreria js, css o theme. Per più inclusioni di tipi diversi, ad esempio, js e css, questo tag deve essere utilizzato più volte in jsp. Questo tag è un wrapper di convenienza intorno all&#39;interfaccia del servizio `com.day.cq.widget.HtmlLibraryManager`.

Ha i seguenti attributi:

**categorie** - Elenco di categorie libreria client separate da virgole. Sono incluse tutte le librerie JavaScript e CSS per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema** - Elenco di categorie libreria client separate da virgole. Sono incluse tutte le librerie relative al tema (sia CSS che JS) per le categorie specificate. Il nome del tema viene estratto dalla richiesta.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js** - Elenco di categorie di librerie client separate da virgole. Sono incluse tutte le librerie JavaScript per le categorie specificate.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** - Elenco di categorie di librerie client separate da virgole. Sono incluse tutte le librerie CSS per le categorie specificate.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**a tema** - Deve essere incluso un flag che indica solo le librerie a tema o non a tema. Se omesso, vengono inclusi entrambi i set. Si applica solo alle inclusioni JS pure o CSS (non per le categorie o i temi).

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

### &lt;cq:defineObjects> {#cq-defineobjects}

Il tag `<cq:defineObjects>` espone i seguenti oggetti di script utilizzati regolarmente a cui può fare riferimento lo sviluppatore. Espone inoltre gli oggetti definiti dal tag [`<sling:defineObjects>`](#amp-lt-sling-defineobjects).

**componentContext**

* l’oggetto contesto componente corrente della richiesta (com.day.cq.wcm.api.components.ComponentContext interface).

**componente**

* l’oggetto componente AEM corrente della risorsa corrente (com.day.cq.wcm.api.components.Component interface).

**currentDesign**

* l&#39;oggetto design corrente della pagina corrente (com.day.cq.wcm.api.designer.Design interface).

**currentPage**

* l’oggetto pagina WCM AEM corrente (com.day.cq.wcm.api.Page interface).

**currentStyle**

* oggetto style corrente della cella corrente (com.day.cq.wcm.api.designer.Style interface).

**designer**

* oggetto designer utilizzato per accedere alle informazioni di progettazione (com.day.cq.wcm.api.designer.Designer interface).

**editContext**

* l’oggetto contesto di modifica del componente AEM (com.day.cq.wcm.api.components.EditContext interface).

**gestione pagine**

* l’oggetto gestore pagine per le operazioni a livello di pagina (com.day.cq.wcm.api.PageManager interface).

**proprietàPagina**

* l’oggetto proprietà della pagina corrente (org.apache.sling.api.resource.ValueMap).

**proprietà**

* l’oggetto proprietà della risorsa corrente (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* oggetto design della pagina delle risorse (com.day.cq.wcm.api.designer.Design interface).

**resourcePage**

* l’oggetto pagina della risorsa (com.day.cq.wcm.api.Page interface).
* Ha i seguenti attributi:

**nomeRichiesta**

* ereditato da sling

**nomeRisposta**

* ereditato da sling

**nomeRisorsa**

* ereditato da sling

**nomeNodo**

* ereditato da sling

**nomeRegistro**

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

**nomeComponente**

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
>Quando il file `/libs/foundation/global.jsp` è incluso nello script, il tag `<cq:defineObjects />` viene incluso automaticamente.

### &lt;cq:requestURL> {#cq-requesturl}

Il tag `<cq:requestURL>` scrive l&#39;URL della richiesta corrente in JspWriter. I due tag [`<cq:addParam>`](#amp-lt-cq-addparam) e [`<cq:removeParam>`](#amp-lt-cq-removeparam) e possono essere utilizzati all&#39;interno del corpo di questo tag per modificare l&#39;URL della richiesta corrente prima che venga scritto.

Consente di creare collegamenti alla pagina corrente con parametri diversi. Ad esempio, consente di trasformare la richiesta:

`mypage.html?mode=view&query=something` in `mypage.html?query=something`.

L&#39;utilizzo di `addParam` o `removeParam` modifica solo l&#39;occorrenza del parametro specificato, mentre tutti gli altri parametri non vengono modificati.

`<cq:requestURL>` non ha alcun attributo.

Esempi:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

Il tag `<cq:addParam>` aggiunge un parametro di richiesta con il nome e il valore specificati al tag [`<cq:requestURL>`](#amp-lt-cq-requesturl) che lo racchiude.

Ha i seguenti attributi:

**nome**

* nome del parametro da aggiungere

**valore**

* valore del parametro da aggiungere

**Esempio:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

Il tag `<cq:removeParam>` rimuove un parametro di richiesta con il nome e il valore specificati dal tag [`<cq:requestURL>`](#amp-lt-cq-requesturl) che lo racchiude. Se non viene fornito alcun valore, vengono rimossi tutti i parametri con il nome specificato.

Ha i seguenti attributi:

**nome**

* nome del parametro da rimuovere

Esempio:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Libreria tag Sling {#sling-tag-library}

La libreria di tag Sling contiene utili funzioni Sling.

Quando utilizzi la libreria di tag Sling nello script, lo script deve iniziare con il seguente codice:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Quando il file `/libs/foundation/global.jsp` è incluso nello script, la libreria a dischi Sling viene dichiarata automaticamente.

### &lt;sling:include> {#sling-include}

Il tag `<sling:include>` include una risorsa nella pagina corrente.

Ha i seguenti attributi:

**scarica**

* Valore booleano che definisce se eseguire il flushing dell’output prima di includere la destinazione.

**risorsa**

* Oggetto risorsa da includere nell’elaborazione della richiesta corrente. Specificare una risorsa o un percorso. Se vengono specificati entrambi, la risorsa ha la precedenza.

**percorso**

* Percorso dell’oggetto risorsa da includere nell’elaborazione della richiesta corrente. Se il percorso è relativo, viene aggiunto al percorso della risorsa corrente il cui script include la risorsa specificata. Specificare una risorsa o un percorso. Se vengono specificati entrambi, la risorsa ha la precedenza.

**tiporisorsa**

* Tipo di risorsa della risorsa da includere. Se il tipo di risorsa è impostato, il percorso deve essere il percorso esatto di un oggetto risorsa: in questo caso, l’aggiunta di parametri, selettori ed estensioni al percorso non è supportata.
* Se la risorsa da includere è specificata con l’attributo path che non può essere risolto in una risorsa, il tag può creare un oggetto risorsa sintetico fuori dal percorso e da questo tipo di risorsa.

**replaceSelectors**

* Durante l’invio, i selettori vengono sostituiti con il valore di questo attributo.

**addSelectors**

* Durante l’invio, il valore di questo attributo viene aggiunto ai selettori.

**replaceSuffix**

* Durante l’invio, il suffisso viene sostituito dal valore di questo attributo.

>[!NOTE]
>
>La risoluzione della risorsa e dello script inclusi nel tag `<sling:include>` è la stessa di una normale risoluzione URL Sling. Per impostazione predefinita, i selettori, l’estensione e così via della richiesta corrente vengono utilizzati anche per lo script incluso. Possono essere modificate tramite gli attributi tag: ad esempio, `replaceSelectors="foo.bar"` consente di sovrascrivere i selettori.

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

Il tag `<sling:defineObjects>` espone i seguenti oggetti di script, utilizzati regolarmente, a cui lo sviluppatore può fare riferimento:

**slingRequest**

* L’oggetto SlingHttpServletRequest, che fornisce l’accesso alle informazioni dell’intestazione della richiesta HTTP - estende la richiesta standard HttpServletRequest - e fornisce l’accesso a elementi specifici di Sling come la risorsa, le informazioni sul percorso e il selettore.

**slingResponse**

* Oggetto SlingHttpServletResponse, che fornisce accesso alla risposta HTTP creata dal server. È lo stesso di HttpServletResponse da cui si estende.**richiesta**
* L’oggetto richiesta JSP standard che è un HttpServletRequest puro.**risposta**
* L’oggetto di risposta JSP standard che è un HttpServletResponse puro.

**resourceResolver**

* Oggetto ResourceResolver corrente. È lo stesso di slingRequest.getResourceResolver()

.**sling**

* Oggetto SlingScriptHelper contenente metodi di convenienza per gli script, principalmente sling.include(&#39;/some/other/resource&#39;) per includere le risposte di altre risorse all&#39;interno di questa risposta (ad esempio, incorporando snippet HTML di intestazione) e sling.getService(foo.bar.Service.class) per recuperare i servizi OSGi disponibili in Sling (notazione di classe a seconda del linguaggio di script).

**risorsa**

* l’oggetto Resource corrente da gestire, a seconda dell’URL della richiesta. È lo stesso di slingRequest.getResource().

**currentNode**

* Se la risorsa corrente punta a un nodo JCR (come in genere avviene in Sling), consente l’accesso diretto all’oggetto Node. In caso contrario, l’oggetto non è definito.

**log**

* Fornisce un logger SLF4J per la registrazione al sistema di registro Sling dall’interno di script, ad esempio log.info(&quot;Executing my script&quot;).

* Ha i seguenti attributi:

**nomeRichiesta**

**nomeRisposta**

**nomeNodo**

l **ogName resourceResolverName**

**slingName**

**Esempio:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## Libreria tag JSTL {#jstl-tag-library}

La [Libreria tag standard per pagine JavaServer](https://www.oracle.com/java/technologies/java-server-tag-library.html) contiene molti tag utili e standard. Le taglib core, formattazione e funzioni sono definite da `/libs/foundation/global.jsp` come mostrato nello snippet seguente.

### Estratto di /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Dopo aver importato il file `/libs/foundation/global.jsp` come descritto in precedenza, è possibile utilizzare i prefissi `c`, `fmt` e `fn` per accedere a tali taglib. La documentazione ufficiale di JSTL è disponibile all&#39;indirizzo [Esercitazione Java™ EE 5 - JavaServer Pages Standard Tag Library](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
