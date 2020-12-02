---
title: Utilizzo di adattatori Sling
seo-title: Utilizzo di adattatori Sling
description: Sling offre un pattern di adattatore per tradurre facilmente gli oggetti che implementano l'interfaccia Adattabile
seo-description: Sling offre un pattern di adattatore per tradurre facilmente gli oggetti che implementano l'interfaccia Adattabile
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
translation-type: tm+mt
source-git-commit: 36cc5ca0de9ae2933a0d7585a00f26cc984d24db
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 1%

---


# Utilizzo di adattatori Sling{#using-sling-adapters}

[](https://sling.apache.org) Slingoffer un  [Adapter ](https://sling.apache.org/site/adapters.html) trasforma in modo conveniente gli oggetti che implementano l&#39;interfaccia  [](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) Adaptable. Questa interfaccia fornisce un metodo generico [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) che tradurrà l&#39;oggetto nel tipo di classe passato come argomento.

Ad esempio, per tradurre un oggetto Resource in un oggetto Node corrispondente, è sufficiente eseguire le operazioni seguenti:

```java
Node node = resource.adaptTo(Node.class);
```

## Casi di utilizzo {#use-cases}

Esistono i seguenti casi di utilizzo:

* Ottenete oggetti specifici per l&#39;implementazione.

   Ad esempio, un&#39;implementazione basata su JCR dell&#39;interfaccia generica [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) fornisce l&#39;accesso al JCR sottostante [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Creazione di collegamenti per oggetti che richiedono il passaggio di oggetti contestuali interni.

   Ad esempio, l&#39;elemento [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) basato su JCR contiene un riferimento all&#39;elemento [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html) della richiesta, che a sua volta è necessario per molti oggetti che funzioneranno in base alla sessione di richiesta, ad esempio [`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) o [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html).

* Collegamento ai servizi.

   Un caso raro - `sling.getService()` è anche semplice.

### Valore restituito Null {#null-return-value}

`adaptTo()` può restituire null.

I motivi di tale scelta sono diversi, tra cui:

* l&#39;implementazione non supporta il tipo di destinazione
* un gestore di schede che gestisce questo caso non è attivo (ad esempio a causa di riferimenti di servizio mancanti)
* condizione interna non riuscita
* il servizio non è disponibile

È importante gestire il caso nullo in modo corretto. Per i rendering jsp potrebbe essere accettabile che il jsp non riesca se si traduce in una parte vuota del contenuto.

### Cache {#caching}

Per migliorare le prestazioni, le implementazioni possono memorizzare nella cache l&#39;oggetto restituito da una chiamata `obj.adaptTo()`. Se `obj` è lo stesso, l&#39;oggetto restituito è lo stesso.

Questa memorizzazione nella cache viene eseguita per tutti i casi basati su `AdapterFactory`.

Tuttavia, non esiste una regola generale: l&#39;oggetto potrebbe essere una nuova istanza o una esistente. Ciò significa che non potete fare affidamento su entrambi i comportamenti. È quindi importante, soprattutto all&#39;interno di `AdapterFactory`, che gli oggetti siano riutilizzabili in questo scenario.

### Come funziona {#how-it-works}

Esistono diversi modi in cui `Adaptable.adaptTo()` può essere implementato:

* dall&#39;oggetto stesso; implementazione del metodo stesso e mappatura a determinati oggetti.
* Tramite un [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), che può mappare oggetti arbitrari.

   Gli oggetti devono comunque implementare l&#39;interfaccia `Adaptable` ed estendere [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (che trasmette la chiamata `adaptTo` a un gestore di adattatori centrali).

   Questo consente di inserire i ganci nel meccanismo `adaptTo` per le classi esistenti, ad esempio `Resource`.

* Una combinazione di entrambi.

Per il primo caso, javadocs può indicare quali `adaptTo-targets` sono possibili. Tuttavia, per sottoclassi specifiche come la risorsa basata su JCR, spesso ciò non è possibile. In quest&#39;ultimo caso, le implementazioni di `AdapterFactory` fanno generalmente parte delle classi private di un bundle e quindi non sono esposte in un&#39;API client, né sono elencate in javadocs. In teoria, sarebbe possibile accedere a tutte le `AdapterFactory` implementazioni dal runtime di [OSGi](/help/sites-deploying/configuring-osgi.md) servizio e vedere le relative configurazioni &quot;adaptables&quot; (origini e destinazioni), ma non mapparle l&#39;una sull&#39;altra. Alla fine, questo dipende dalla logica interna, che deve essere documentata. Di qui il riferimento.

## Riferimento {#reference}

### Sling {#sling}

[**Adattamento**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) risorsa a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>Se si tratta di una risorsa basata su nodo JCR o di una proprietà JCR che fa riferimento a un nodo.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Proprietà</a></td>
   <td>Se si tratta di una risorsa basata su proprietà JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Elemento</a></td>
   <td>Se si tratta di una risorsa basata su JCR (nodo o proprietà).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Mappa</a></td>
   <td>Restituisce una mappa delle proprietà, se si tratta di una risorsa basata su nodo JCR (o di altre mappe dei valori di supporto delle risorse).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Restituisce una mappa pratica delle proprietà, se si tratta di una risorsa basata su nodo JCR (o di altre mappe di valore di supporto delle risorse). Può essere anche ottenuto (più semplicemente) utilizzando <br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> (gestisce maiuscole/minuscole, ecc.).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">EreditanceValueMap</a></td>
   <td>Estensione di <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> che consente di tenere conto della gerarchia delle risorse nella ricerca delle proprietà.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModificabileValueMap</a></td>
   <td>Un'estensione di <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>, che consente di modificare le proprietà di tale nodo.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Restituisce il contenuto binario di una risorsa file (se si tratta di una risorsa basata su nodo JCR e il tipo di nodo è <code>nt:file</code> o <code>nt:resource</code>; se si tratta di una risorsa bundle; il contenuto del file, se si tratta di una risorsa del file system) o i dati di una risorsa di proprietà JCR binaria.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Restituisce un URL alla risorsa (URL del repository di questo nodo, se si tratta di una risorsa basata su nodo JCR); URL bundle Jar se si tratta di una risorsa bundle; URL del file (se si tratta di una risorsa del file system).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">File</a></td>
   <td>Se si tratta di una risorsa del file system.</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Se la risorsa è uno script (ad esempio, un file jsp) per il quale un motore di script è registrato con sling.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>Se la risorsa è uno script (ad esempio, un file jsp) per il quale un motore di script è registrato con sling o se si tratta di una risorsa servlet.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"></a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">StringBooleanLongDoubleCalendarValueString[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>Restituisce i valori se si tratta di una risorsa basata su proprietà JCR (e il valore corrisponde).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Se si tratta di una risorsa basata su nodo JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html">Pagina</a></td>
   <td>Se si tratta di una risorsa basata su nodo JCR e il nodo è <code>cq:Page</code> (o <code>cq:PseudoPage</code>).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html">Componente</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:Component</code>.</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Design.html">Progettazione</a></td>
   <td>Se si tratta di un nodo di progettazione (<code>cq:Page</code>).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html">Modello</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:Template</code>.</td>
  </tr>  
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:Template</code>.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">Risorsa</a></td>
   <td>Se si tratta di una risorsa nodo dam:Asset.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">Rappresentazione</a></td>
   <td>Se si tratta di una rappresentazione dam:Asset (nt:file sotto la cartella di rappresentazione di una dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html">Tag</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:Tag</code>.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Basato sulla sessione JCR se si tratta di una risorsa basata su JCR e se l'utente dispone delle autorizzazioni per accedere a UserManager.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizzabile</a></td>
   <td>L’Autorizzazione è l’interfaccia di base comune per Utente e Gruppo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a></td>
   <td>Utente è uno speciale autorizzabile che può essere autenticato e rappresentato.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>Cerca sotto la risorsa (o utilizza setSearchIn()) se si tratta di una risorsa basata su JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Stato del flusso di lavoro per il nodo payload pagina/flusso di lavoro specificato.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>Stato della replica per la risorsa specificata o il relativo nodo secondario jcr:content (selezionato per primo).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Restituisce una risorsa connettore adattata per alcuni tipi, se si tratta di una risorsa basata su nodo JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">Configurazione</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:ContentSyncConfig</code>.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Se si trova sotto una risorsa nodo <code>cq:ContentSyncConfig</code>.</td>
  </tr>
 </tbody>
</table>

[**ResourceResolverts si adatta a:**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) 

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Sessione</a></td>
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
   <td>In base alla sessione JCR, se si tratta di un risolutore di risorse basato su JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>In base alla sessione JCR, se si tratta di un risolutore di risorse basato su JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager fornisce l'accesso e i mezzi per mantenere gli oggetti autorizzabili, ad esempio utenti e gruppi. UserManager è associato a una sessione specifica.
   </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizzabile</a> </td>
   <td>L’utente corrente.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a><br /> </td>
   <td>L’utente corrente.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>Per esternalizzare gli URL assoluti, anche con l'oggetto di richiesta.<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequests si adatta a:**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) 

Nessuna destinazione ancora, ma implementa Adattabile e potrebbe essere utilizzato come origine in un AdapterFactory personalizzato.

[**SlingHttpServletResponsesi adatta a:**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) 

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>Se si tratta di una risposta sling rewriter.</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Pageadts ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)** si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Risorsa</a><br /> </td>
   <td>Risorsa della pagina.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Risorsa con etichetta (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>Nodo della pagina.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tutto ciò a cui è possibile adattare la risorsa della pagina.</td>
  </tr>
 </tbody>
</table>

**[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)** Componenti si adattano a:

| [Risorsa](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Risorsa del componente. |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | Risorsa con etichetta (== this). |
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del componente. |
| ... | Tutto ciò a cui la risorsa del componente può essere adattata. |

**[Modello ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)** adattabile a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Risorsa</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Risorsa del modello.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Risorsa con etichetta (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>Nodo di questo modello.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tutto ciò a cui può essere adattata la risorsa del modello.</td>
  </tr>
 </tbody>
</table>

#### Sicurezza {#security}

**Autorizzabili**,  **** utenti e  **** gruppi di utenti possono:

| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Restituisce il nodo principale utente/gruppo. |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | Restituisce lo stato di replica per il nodo principale utente/gruppo. |

#### DAM {#dam}

**Le** risorse si adattano a:

| [Risorsa](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Risorsa della risorsa. |
|---|---|
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo della risorsa. |
| ... | Tutto ciò a cui la risorsa della risorsa può essere adattata. |

#### Assegnazione tag {#tagging}

**I** tag si adattano a:

| [Risorsa](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Risorsa del tag. |
|---|---|
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del tag. |
| ... | Tutto ciò a cui la risorsa del tag può essere adattata. |

#### Altro {#other}

Inoltre Sling / JCR / OCM fornisce un ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` per gli oggetti OCM personalizzati ([Object Content Mapping](https://jackrabbit.apache.org/object-content-mapping.html)).
