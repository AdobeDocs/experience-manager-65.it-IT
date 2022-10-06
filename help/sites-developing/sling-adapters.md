---
title: Utilizzo di adattatori Sling
seo-title: Using Sling Adapters
description: Sling offre un pattern di adattatore per tradurre in modo conveniente gli oggetti che implementano l'interfaccia adattabile
seo-description: Sling offers an Adapter pattern to conveniently translate objects that implement the Adaptable interface
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 13%

---

# Utilizzo di adattatori Sling{#using-sling-adapters}

[Sling](https://sling.apache.org) offre [Pattern di adattatore](https://sling.apache.org/site/adapters.html) per tradurre gli oggetti che implementano [Adattabile](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) interfaccia. Questa interfaccia fornisce un generico [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) metodo che tradurrà l&#39;oggetto nel tipo di classe passato come argomento.

Ad esempio, per tradurre un oggetto Resource all&#39;oggetto Node corrispondente, è sufficiente eseguire le operazioni seguenti:

```java
Node node = resource.adaptTo(Node.class);
```

## Casi d&#39;uso {#use-cases}

Esistono i seguenti casi d’uso:

* Ottenere oggetti specifici per l’implementazione.

   Ad esempio, un’implementazione basata su JCR del generico [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) L&#39;interfaccia fornisce l&#39;accesso al JCR sottostante [`Node`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Creazione rapida di oggetti che richiedono il passaggio di oggetti contestuali interni.

   Ad esempio, il modello basato su JCR [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) contiene un riferimento al [`JCR Session`](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html), che a sua volta è necessario per molti oggetti che funzioneranno in base a tale sessione di richiesta, come [`PageManager`](https://helpx.adobe.com/it/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) o [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html).

* Collegamento ai servizi.

   Un caso raro - `sling.getService()` è anche semplice.

### Valore restituito nullo {#null-return-value}

`adaptTo()` può restituire null.

Ci sono varie ragioni per questo, tra cui:

* l&#39;implementazione non supporta il tipo di destinazione
* un adattatore che gestisce questo caso in fabbrica non è attivo (ad esempio a causa di riferimenti di servizio mancanti)
* condizione interna non riuscita
* servizio non disponibile

È importante gestire il caso null in modo corretto. Per i rendering jsp potrebbe essere accettabile che jsp non riesca se questo si traduce in un contenuto vuoto.

### Memorizzazione in cache {#caching}

Per migliorare le prestazioni, le implementazioni sono libere di memorizzare nella cache l&#39;oggetto restituito da un `obj.adaptTo()` chiama. Se la `obj` è lo stesso, l&#39;oggetto restituito è lo stesso.

Questa memorizzazione in cache viene eseguita per tutti `AdapterFactory` casi basati.

Tuttavia, non esiste una regola generale: l&#39;oggetto potrebbe essere una nuova istanza o una esistente. Ciò significa che non puoi affidarti a entrambi i comportamenti. Quindi è importante, soprattutto all&#39;interno `AdapterFactory`, gli oggetti sono riutilizzabili in questo scenario.

### Come funziona {#how-it-works}

Ci sono diversi modi per `Adaptable.adaptTo()` può essere implementato:

* dall&#39;oggetto stesso; implementazione del metodo stesso e mappatura a determinati oggetti.
* Da [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), che può mappare oggetti arbitrari.

   Gli oggetti devono ancora implementare il `Adaptable` e deve estendere [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (che passa `adaptTo` chiamare un gestore di adattatori centrali).

   Questo consente agli hook di `adaptTo` meccanismo per le classi esistenti, ad esempio `Resource`.

* Una combinazione di entrambi.

Per il primo caso, i javadocs possono indicare cosa `adaptTo-targets` sono possibili. Tuttavia, per sottoclassi specifiche come la risorsa basata su JCR, spesso questo non è possibile. In quest&#39;ultimo caso, l&#39;attuazione `AdapterFactory` in genere fanno parte delle classi private di un bundle e quindi non sono esposte in un&#39;API client, né sono elencate in javadocs. Teoricamente, sarebbe possibile accedere a tutti `AdapterFactory` implementazioni dal [OSGi](/help/sites-deploying/configuring-osgi.md) runtime di servizio e guarda le loro configurazioni &quot;adaptables&quot; (origini e destinazioni), ma non per mapparle tra di loro. Alla fine, questo dipende dalla logica interna, che deve essere documentata. Da qui questo riferimento.

## Riferimento {#reference}

### Sling {#sling}

[**Risorsa**](https://helpx.adobe.com/it/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Se si tratta di una risorsa basata su nodo JCR o di una proprietà JCR che fa riferimento a un nodo.</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Proprietà</a></td>
   <td>Se si tratta di una risorsa basata su JCR-property.</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Elemento</a></td>
   <td>Se si tratta di una risorsa basata su JCR (nodo o proprietà).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Mappa</a></td>
   <td>Restituisce una mappa delle proprietà, se si tratta di una risorsa basata su un nodo JCR (o di altre risorse che supportano le mappe dei valori).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Restituisce una mappa pratica delle proprietà, se si tratta di una risorsa basata su un nodo JCR (o di altre risorse che supportano le mappe dei valori). Può essere ottenuto anche (più semplicemente) utilizzando<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> (gestisce lettere maiuscole, ecc.).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">EreditarietàValueMap</a></td>
   <td>Proroga <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> che consente di tenere conto della gerarchia delle risorse nella ricerca delle proprietà.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModificabileValueMap</a></td>
   <td>L'estensione del <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>, che ti consente di modificare le proprietà di quel nodo.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Restituisce il contenuto binario di una risorsa file (se si tratta di una risorsa basata su nodo JCR e il tipo di nodo è <code>nt:file</code> o <code>nt:resource</code>; se si tratta di una risorsa di bundle; il contenuto del file (se si tratta di una risorsa del file system) o i dati di una risorsa di proprietà JCR binaria.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Restituisce un URL alla risorsa (URL del repository di questo nodo se si tratta di una risorsa basata su nodo JCR; URL del bundle jar se si tratta di una risorsa del bundle; URL del file se si tratta di una risorsa del file system).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">File</a></td>
   <td>Se si tratta di una risorsa del file system.</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Se questa risorsa è uno script (ad esempio un file jsp) per il quale un motore di script è registrato con sling.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>Se questa risorsa è uno script (ad esempio un file jsp) per il quale un motore di script è registrato con sling o se si tratta di una risorsa servlet.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">Stringa</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Booleano</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Lunga</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html">Doppio</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendario</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Valore</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendario[]</a><br /> <a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>Restituisce i valori se si tratta di una risorsa basata su JCR-property (e il valore si adatta).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Se si tratta di una risorsa basata su nodo JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html">Pagina</a></td>
   <td>Se si tratta di una risorsa basata su nodo JCR e il nodo è un <code>cq:Page</code> o <code>cq:PseudoPage</code>).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html">Componente</a></td>
   <td>Se si tratta di un <code>cq:Component</code> risorsa nodo.</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Design.html">Design</a></td>
   <td>Se si tratta di un nodo di progettazione (<code>cq:Page</code>).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html">Modello</a></td>
   <td>Se si tratta di un <code>cq:Template</code> risorsa nodo.</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>Se si tratta di un <code>cq:Template</code> risorsa nodo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">Risorsa</a></td>
   <td>Se si tratta di una risorsa nodo dam:Asset.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">Rappresentazione</a></td>
   <td>Se si tratta di un rendering dam:Asset (nt:file sotto la cartella di rendering di un dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">Tag</a></td>
   <td>Se si tratta di un <code>cq:Tag</code> risorsa nodo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Basato sulla sessione JCR se si tratta di una risorsa basata su JCR e l'utente dispone delle autorizzazioni per accedere a UserManager.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizzabile</a></td>
   <td>Authorizable è l’interfaccia di base comune per Utente e Gruppo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a></td>
   <td>Utente è uno speciale Authorizable che può essere autenticato e rappresentato.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>Cerca sotto la risorsa (o utilizza setSearchIn()) se si tratta di una risorsa basata su JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Stato del flusso di lavoro per il nodo di payload pagina/flusso di lavoro specificato.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>Stato di replica per la risorsa specificata o il relativo sottonodo jcr:content (selezionato per primo).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Restituisce una risorsa di connettore adattata per alcuni tipi, se si tratta di una risorsa basata su nodo JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">Configurazione</a></td>
   <td>Se si tratta di un <code>cq:ContentSyncConfig</code> risorsa nodo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Se si trova sotto a <code>cq:ContentSyncConfig</code> risorsa nodo.</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://helpx.adobe.com/it/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Sessione</a></td>
   <td>La sessione JCR della richiesta, se si tratta di un risolutore di risorse basato su JCR (predefinito).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>Basato sulla sessione JCR, se si tratta di un risolutore di risorse basato su JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>Basato sulla sessione JCR, se si tratta di un risolutore di risorse basato su JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager fornisce l'accesso e i mezzi per gestire oggetti autorizzabili, ad esempio utenti e gruppi. UserManager è associato a una sessione specifica.
   </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizzabile</a> </td>
   <td>Utente corrente.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a><br /> </td>
   <td>Utente corrente.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Esternalizzatore</a></td>
   <td>Per esternalizzare gli URL assoluti, anche con l’oggetto di richiesta.<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) si adatta a:

Nessuna destinazione, ma implementa Adattabile e può essere utilizzato come origine in un AdapterFactory personalizzato.

[**SlingHttpServletResponse**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>Se si tratta di una risposta sling rewriter.</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Pagina](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>Risorsa della pagina.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Risorsa con etichetta (== this).</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo della pagina.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tutto ciò a cui la risorsa della pagina può essere adattata.</td>
  </tr>
 </tbody>
</table>

**[Componente](https://helpx.adobe.com/it/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** si adatta a:

| [Risorsa](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Risorsa del componente. |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | Risorsa con etichetta (== this). |
| [Nodo](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del componente. |
| ... | Tutto ciò a cui può essere adattata la risorsa del componente. |

**[Modello](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Risorsa del modello.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Risorsa con etichetta (== this).</td>
  </tr>
  <tr>
   <td><a href="https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo di questo modello.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tutto ciò a cui può essere adattata la risorsa del modello.</td>
  </tr>
 </tbody>
</table>

#### Sicurezza {#security}

**Autorizzabile**, **Utente** e **Gruppo** adattarsi a:

| [Nodo](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Restituisce il nodo principale utente/gruppo. |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | Restituisce lo stato di replica per il nodo home utente/gruppo. |

#### DAM {#dam}

**Risorsa** si adatta a:

| [Risorsa](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Risorsa della risorsa. |
|---|---|
| [Nodo](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo della risorsa. |
| ... | Tutto ciò a cui la risorsa può essere adattata. |

#### Assegnazione tag {#tagging}

**Tag** si adatta a:

| [Risorsa](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Risorsa del tag . |
|---|---|
| [Nodo](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del tag. |
| ... | Tutto ciò a cui la risorsa del tag può essere adattata. |

#### Altro {#other}

Inoltre, Sling / JCR / OCM fornisce ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` per OCM personalizzata ([Mappatura del contenuto degli oggetti](https://jackrabbit.apache.org/object-content-mapping.html)).
