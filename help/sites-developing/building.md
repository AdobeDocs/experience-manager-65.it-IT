---
title: Creazione di tag in un’applicazione AEM
seo-title: Building Tagging into an AEM Application
description: Utilizzare i tag a livello di programmazione o estenderli all’interno di un’applicazione AEM personalizzata
seo-description: Programmatically work with tags or extending tags within a custom AEM application
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: 325af649564d93beedfc762a8f5beacec47b1641
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 0%

---

# Creazione di tag in un’applicazione AEM{#building-tagging-into-an-aem-application}

Per lavorare in modo programmatico con i tag o estenderli all’interno di un’applicazione AEM personalizzata, questa pagina descrive l’utilizzo di

* [API di assegnazione tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

che interagisce con il

* [Framework di tag](/help/sites-developing/framework.md)

Per informazioni correlate sull’assegnazione tag, consulta:

* [Amministrazione dei tag](/help/sites-administering/tags.md) per informazioni sulla creazione e la gestione dei tag e sui tag di contenuto applicati.
* [Utilizzo dei tag](/help/sites-authoring/tags.md) per informazioni sull’assegnazione tag al contenuto.

## Panoramica dell’API di assegnazione tag {#overview-of-the-tagging-api}

L&#39;attuazione del [framework di assegnazione tag](/help/sites-developing/framework.md) in AEM consente la gestione di tag e contenuti tag utilizzando l’API JCR. TagManager garantisce che i tag immessi come valori sul `cq:tags` La proprietà string array non è duplicata, rimuove i TagID che puntano a tag non esistenti e aggiorna i TagID per i tag spostati o uniti. TagManager utilizza un listener di osservazione JCR che ripristina eventuali modifiche non corrette. Le classi principali sono [com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html) pacchetto:

* JcrTagManagerFactory: restituisce un’implementazione basata su JCR di un `TagManager`. È l’implementazione di riferimento dell’API di assegnazione tag.
* `TagManager` : consente di risolvere e creare tag in base a percorsi e nomi.
* `Tag` : definisce l’oggetto tag.

### Ottenere un TagManager basato su JCR {#getting-a-jcr-based-tagmanager}

Per recuperare un’istanza di TagManager, è necessario disporre di un JCR `Session` e chiamare `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

Nel tipico contesto Sling, puoi anche adattarti a una `TagManager` dal `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recupero di un oggetto Tag {#retrieving-a-tag-object}

A `Tag` possono essere recuperati tramite `TagManager`, risolvendo un tag esistente o creandone uno:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Per l’implementazione basata su JCR, che mappa `Tags` su JCR `Nodes`, puoi utilizzare direttamente Sling `adaptTo` se si dispone della risorsa (ad esempio, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Mentre un tag può essere convertito solo *da *una risorsa (non un nodo), un tag può essere convertito *sia in un nodo che in una risorsa:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adattamento diretto da `Node` a `Tag` non è possibile, perché `Node` non implementa Sling `Adaptable.adaptTo(Class)` metodo.

### Recupero e impostazione dei tag {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Ricerca di tag {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>Il valore `RangeIterator` da utilizzare è:
>
>`com.day.cq.commons.RangeIterator`

### Eliminazione dei tag {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replica dei tag {#replicating-tags}

È possibile utilizzare il servizio di replica ( `Replicator`) con tag perché i tag sono di tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Assegnazione di tag sul lato client {#tagging-on-the-client-side}

Widget modulo `CQ.tagging.TagInputField` è per l’immissione di tag. Dispone di un menu a comparsa per selezionare da tag esistenti, include il completamento automatico e molte altre funzioni. Il suo xtype è `tags`.

## Tag Garbage Collector {#the-tag-garbage-collector}

Il garbage collector dei tag è un servizio in background che consente di pulire i tag nascosti e non utilizzati. Di seguito sono riportati i tag nascosti e non utilizzati `/content/cq:tags` che hanno un `cq:movedTo` e non vengono utilizzati in un nodo di contenuto, poiché hanno un conteggio pari a zero. Utilizzando questo processo di eliminazione lenta, il nodo del contenuto (ovvero `cq:tags` ) non deve essere aggiornata come parte dell’operazione di spostamento o unione. I riferimenti in `cq:tags` vengono aggiornate automaticamente quando `cq:tags` viene aggiornata, ad esempio, tramite la finestra di dialogo proprietà pagina.

Il garbage collector dei tag viene eseguito per impostazione predefinita una volta al giorno. Puoi configurarlo in:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Ricerca di tag ed elenco di tag {#tag-search-and-tag-listing}

La ricerca dei tag e l’elenco dei tag funzionano come segue:

* La ricerca di TagID cerca i tag che hanno la proprietà `cq:movedTo` impostato su TagID e segue attraverso `cq:movedTo` TagID.

* La ricerca di Titolo tag cerca solo i tag che non hanno un `cq:movedTo` proprietà.

## Tag in lingue diverse {#tags-in-different-languages}

Come descritto nella documentazione per l’amministrazione dei tag, nella sezione [Gestione dei tag in lingue diverse](/help/sites-administering/tags.md#managing-tags-in-different-languages), un tag `title`possono essere definiti in diverse lingue. Al nodo del tag viene quindi aggiunta una proprietà sensibile alla lingua. Questa proprietà ha il formato `jcr:title.<locale>`ad esempio: `jcr:title.fr` per la traduzione francese. Il `<locale>` deve essere una stringa internazionale ISO minuscola e utilizzare &quot;_&quot; invece di &quot;-&quot;, ad esempio: `de_ch`.

Quando **Animali** viene aggiunto al tag **Prodotti** pagina, il valore `stockphotography:animals` viene aggiunto alla proprietà `cq:tags` del nodo /content/geometrixx/en/products/jcr:content. Viene fatto riferimento alla traduzione dal nodo del tag.

L’API lato server ha localizzato `title`Metodi relativi a:

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Locale locale)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Lingua locale)
   * getTitlePath(impostazioni locali)

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, impostazioni locali)
   * createTagByTitle(String tagTitlePath, impostazioni locali)
   * resolveByTitle(String tagTitlePath, impostazioni locali)

In AEM, la lingua può essere ottenuta o dalla lingua della pagina o dalla lingua dell’utente:

* per recuperare la lingua della pagina in una JSP:

   * `currentPage.getLanguage(false)`

* per recuperare la lingua utente in una JSP:

   * `slingRequest.getLocale()`

Il `currentPage` e `slingRequest` sono disponibili in una JSP tramite [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) tag.

Per i tag, la localizzazione dipende dal contesto come tag `titles`può essere visualizzata nella lingua della pagina, nella lingua dell’utente o in qualsiasi altra lingua.

### Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag {#adding-a-new-language-to-the-edit-tag-dialog}

Nella procedura seguente viene descritto come aggiungere una lingua (finlandese) al **Modifica tag** finestra di dialogo:

1. In entrata **CRXDE**, modifica la proprietà con più valori `languages` del nodo `/content/cq:tags`.

1. Aggiungi `fi_fi` - che rappresenta la lingua finlandese - e salvare le modifiche.

La nuova lingua (finlandese) è ora disponibile nella finestra di dialogo dei tag delle proprietà della pagina e nel **Modifica tag** durante la modifica di un tag in **Assegnazione tag** console.

>[!NOTE]
>
>La nuova lingua deve essere una delle lingue riconosciute dall&#39;AEM. In altre parole, deve essere disponibile come nodo sotto `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>L’installazione di un service pack reimposta la proprietà Languages del nodo /content/cq:tags sui valori predefiniti. Pertanto, è necessario aggiungerlo dalle proprietà prima dell’installazione.
