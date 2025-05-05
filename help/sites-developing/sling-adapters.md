---
title: Utilizzo di adattatori Sling
description: Sling offre un pattern Adapter per tradurre in modo semplice gli oggetti che implementano l'interfaccia Adaptable
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 4%

---

# Utilizzo di adattatori Sling{#using-sling-adapters}

[Sling](https://sling.apache.org) offre un [pattern di adattatore](https://sling.apache.org/documentation/the-sling-engine/adapters.html) per tradurre in modo comodo gli oggetti che implementano l&#39;interfaccia [Adaptable](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29). Questa interfaccia fornisce un metodo [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) generico che converte l&#39;oggetto nel tipo di classe passato come argomento.

Ad esempio, per tradurre un oggetto Resource nell’oggetto Node corrispondente, puoi semplicemente effettuare le seguenti operazioni:

```java
Node node = resource.adaptTo(Node.class);
```

## Casi d’uso {#use-cases}

Sono disponibili i seguenti casi d’uso:

* Ottieni oggetti specifici per l’implementazione.

  Ad esempio, un&#39;implementazione JCR dell&#39;interfaccia generica [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) fornisce l&#39;accesso al JCR sottostante [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Creazione di collegamenti di oggetti che richiedono il passaggio di oggetti contestuali interni.

  Ad esempio, il [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) basato su JCR contiene un riferimento al [`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html) della richiesta, che a sua volta è necessario per molti oggetti che funzioneranno in base alla sessione di richiesta, ad esempio [`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html) o [`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html).

* Collegamento ai servizi.

  Un caso raro - `sling.getService()` è semplice.

### Valore restituito nullo {#null-return-value}

`adaptTo()` restituisce null.

Le ragioni sono diverse, tra cui:

* l’implementazione non supporta il tipo di target
* un adapter factory che gestisce questo caso non è attivo (ad esempio, a causa di riferimenti di servizio mancanti)
* condizione interna non riuscita
* servizio non disponibile

È importante gestire il caso nullo in modo corretto. Per i rendering JSP potrebbe essere accettabile che l’esecuzione di JSP non riesca se si verifica una parte di contenuto vuota.

### Memorizzazione in cache {#caching}

Per migliorare le prestazioni, le implementazioni possono memorizzare nella cache l&#39;oggetto restituito da una chiamata `obj.adaptTo()`. Se `obj` è lo stesso, l&#39;oggetto restituito è lo stesso.

Questa memorizzazione nella cache viene eseguita per tutti i `AdapterFactory` casi basati su.

Tuttavia, non esiste una regola generale: l’oggetto potrebbe essere una nuova istanza o una esistente. Ciò significa che non puoi fare affidamento su entrambi i comportamenti. È quindi importante, soprattutto all&#39;interno di `AdapterFactory`, che gli oggetti siano riutilizzabili in questo scenario.

### Come funziona {#how-it-works}

È possibile implementare `Adaptable.adaptTo()` in vari modi:

* Dall&#39;oggetto stesso, implementando il metodo stesso e mappando a determinati oggetti.
* Da un [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), che può mappare oggetti arbitrari.

  Gli oggetti devono ancora implementare l&#39;interfaccia `Adaptable` e devono estendere [`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (che trasmette la chiamata `adaptTo` a un gestore adapter centrale).

  Consente gli hook nel meccanismo `adaptTo` per le classi esistenti, ad esempio `Resource`.

* Una combinazione di entrambi.

Nel primo caso, i documenti Java™ possono indicare le `adaptTo-targets` possibili. Tuttavia, spesso questo non è possibile per sottoclassi specifiche, come la risorsa basata su JCR. In quest&#39;ultimo caso, le implementazioni di `AdapterFactory` fanno generalmente parte delle classi private di un bundle e quindi non sono esposte in un&#39;API client, né elencate nei documenti Java™. In teoria, sarebbe possibile accedere a tutte le implementazioni di `AdapterFactory` dal runtime del servizio [OSGi](/help/sites-deploying/configuring-osgi.md) e esaminare le relative configurazioni &quot;adattabili&quot; (origini e destinazioni), ma non mapparle tra loro. Alla fine, questo dipende dalla logica interna, che deve essere documentata. Da qui questo riferimento.

## Riferimento {#reference}

### Sling {#sling}

[**La risorsa**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Se si tratta di una risorsa basata su nodo JCR o di una proprietà JCR che fa riferimento a un nodo.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Proprietà</a></td>
   <td>Se si tratta di una risorsa basata su proprietà JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Elemento</a></td>
   <td>Se si tratta di una risorsa basata su JCR (nodo o proprietà)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">Mappa</a></td>
   <td>Restituisce una mappa delle proprietà, se si tratta di una risorsa basata su nodo JCR (o altre mappe di valore di supporto delle risorse)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Restituisce una mappa delle proprietà di facile utilizzo, se si tratta di una risorsa basata su nodo JCR (o su altre mappe di valore di supporto delle risorse). Può anche essere ottenuto (più semplicemente) utilizzando <br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code> (gestisce le maiuscole/minuscole e così via)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>Estensione di <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> che consente di tenere conto della gerarchia delle risorse durante la ricerca delle proprietà</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td>Estensione di <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>, che consente di modificare le proprietà in tale nodo</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Restituisce il contenuto binario di una risorsa file (se si tratta di una risorsa basata su nodo JCR e il tipo di nodo è <code>nt:file</code> o <code>nt:resource</code>; se si tratta di una risorsa bundle; il contenuto del file se si tratta di una risorsa del file system) o i dati di una risorsa proprietà JCR binaria</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Restituisce un URL alla risorsa (URL archivio di questo nodo, se si tratta di una risorsa basata su nodo JCR; URL bundle JAR, se si tratta di una risorsa bundle; URL file, se si tratta di una risorsa del file system)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">File</a></td>
   <td>Se si tratta di una risorsa del file system</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Se questa risorsa è uno script (ad esempio, un file jsp) per il quale un motore di script è registrato con sling</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">Servlet</a></td>
   <td>Se questa risorsa è uno script (ad esempio, un file jsp) per il quale un motore di script è registrato con sling o se si tratta di una risorsa servlet.</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">Stringa</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Booleano</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Lungo</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Doppio</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendario</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Valore</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">Stringa[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Booleano[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Lungo[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendario[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Valore[]</a></td>
   <td>Restituisce i valori se si tratta di una risorsa basata su proprietà JCR (e il valore si adatta).</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Se si tratta di una risorsa basata su nodo JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html">Pagina</a></td>
   <td>Se si tratta di una risorsa basata su nodo JCR e il nodo è un <code>cq:Page</code> (o <code>cq:PseudoPage</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html">Componente</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:Component</code></td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Design.html">Design</a></td>
   <td>Se si tratta di un nodo di progettazione (<code>cq:Page</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html">Modello</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:Template</code></td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:Template</code></td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Asset.html">Risorsa</a></td>
   <td>Se si tratta di una risorsa nodo dam:Asset</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Rendition.html">Rappresentazione</a></td>
   <td>Se si tratta di una rappresentazione dam:Asset (nt:file sotto la cartella di rappresentazione di una dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/Tag.html">Tag</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:Tag</code></td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>In base alla sessione JCR, se si tratta di una risorsa basata su JCR e l’utente dispone delle autorizzazioni per accedere a UserManager</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizzabile</a></td>
   <td>Authorizable è l'interfaccia di base comune per Utente e Gruppo</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a></td>
   <td>L’utente è un Autorizzabile speciale che può essere autenticato e rappresentato</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/SimpleSearch.html">Ricerca semplice</a></td>
   <td>Cerca sotto la risorsa (o usa setSearchIn()) se si tratta di una risorsa basata su JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Stato del flusso di lavoro per il nodo payload pagina/flusso di lavoro specificato</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>Stato della replica per la risorsa specificata o il relativo sottonodo jcr:content (selezionato per primo)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Restituisce una risorsa connettore adattata per alcuni tipi, se si tratta di una risorsa basata su nodo JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">Configurazione</a></td>
   <td>Se si tratta di una risorsa nodo <code>cq:ContentSyncConfig</code></td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Se si trova al di sotto di una risorsa nodo <code>cq:ContentSyncConfig</code></td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceResolver.html) si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Sessione</a></td>
   <td>La sessione JCR della richiesta, se si tratta di un risolutore risorse basato su JCR (impostazione predefinita)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/AssetManager.html">Gestione risorse</a></td>
   <td>In base alla sessione JCR, se si tratta di un risolutore risorse basato su JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>In base alla sessione JCR, se si tratta di un risolutore risorse basato su JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager fornisce l'accesso e i mezzi per gestire gli oggetti autorizzabili, ovvero utenti e gruppi. UserManager è associato a una sessione specifica
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizzabile</a> </td>
   <td>L'utente corrente</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">Utente</a><br /> </td>
   <td>L'utente corrente</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html">Esternalizzatore</a></td>
   <td>Per l'esternalizzazione di URL assoluti, anche senza l'oggetto richiesta<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) si adatta a:

Ancora nessuna destinazione, ma implementa Adaptable e potrebbe essere utilizzato come origine in un AdapterFactory personalizzato.

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">Gestore contenuto</a><br /> (XML)</td>
   <td>Se si tratta di una risposta del rewriter di Sling</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[La pagina](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html)** si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>Risorsa della pagina</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Risorsa con etichetta (== questo)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo della pagina</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tutto ciò a cui può essere adattata la risorsa della pagina</td>
  </tr>
 </tbody>
</table>

**[Il componente](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html)** si adatta a:

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | Risorsa del componente. |
|---|---|
| [RisorsaEtichettata](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html) | Risorsa con etichetta (== questo). |
| [Nodo](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del componente. |
| ... | Tutto ciò a cui può essere adattata la risorsa del componente. |

**[Il modello](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html)** si adatta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">Risorsa</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Risorsa del modello</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Risorsa con etichetta (== questo)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo di questo modello</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tutto ciò a cui può essere adattata la risorsa del modello.</td>
  </tr>
 </tbody>
</table>

#### Sicurezza {#security}

**Authorizable**, **User e &#x200B;** Group** si adattano a:

| [Nodo](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Restituisce il nodo principale dell&#39;utente/gruppo. |
|---|---|
| [StatoReplica](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html) | Restituisce lo stato di replica per il nodo principale utente/gruppo. |

#### DAM {#dam}

**Risorsa** si adatta a:

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | Risorsa della risorsa. |
|---|---|
| [Nodo](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo della risorsa. |
| ... | Tutto ciò a cui può essere adattata la risorsa della risorsa. |

#### Assegnazione dei tag {#tagging}

**Tag** si adatta a:

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | Risorsa del tag. |
|---|---|
| [Nodo](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del tag. |
| ... | Tutto ciò a cui può essere adattata la risorsa del tag. |

#### Altro {#other}

Inoltre, Sling / JCR / OCM fornisce anche un ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` per gli oggetti OCM personalizzati ([Object Content Mapping](https://jackrabbit.apache.org/jcr/object-content-mapping.html)).
