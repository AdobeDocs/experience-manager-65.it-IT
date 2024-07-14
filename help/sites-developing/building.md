---
title: Creazione di tag in un’applicazione AEM
description: Utilizzare i tag a livello di programmazione o estenderli all’interno di un’applicazione AEM personalizzata
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
feature: Developing,Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Creazione di tag in un’applicazione AEM{#building-tagging-into-an-aem-application}

Per lavorare in modo programmatico con i tag o estenderli all’interno di un’applicazione AEM personalizzata, questa pagina descrive l’utilizzo di

* [API di assegnazione tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

che interagisce con il

* [Framework di tag](/help/sites-developing/framework.md)

Per informazioni correlate sull’assegnazione tag, consulta:

* [Amministrazione dei tag](/help/sites-administering/tags.md) per informazioni sulla creazione e la gestione dei tag e sui tag di contenuto applicati.
* [Utilizzo dei tag](/help/sites-authoring/tags.md) per informazioni sui tag del contenuto.

## Panoramica dell’API di assegnazione tag {#overview-of-the-tagging-api}

L&#39;implementazione del [framework dei tag](/help/sites-developing/framework.md) nell&#39;AEM consente la gestione di tag e contenuti di tag tramite l&#39;API JCR. TagManager garantisce che i tag immessi come valori nella proprietà dell&#39;array di stringhe `cq:tags` non siano duplicati, rimuove i TagID che puntano a tag non esistenti e aggiorna i TagID per i tag spostati o uniti. TagManager utilizza un listener di osservazione JCR che ripristina eventuali modifiche non corrette. Le classi principali si trovano nel pacchetto [com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html):

* JcrTagManagerFactory: restituisce un&#39;implementazione basata su JCR di `TagManager`. È l’implementazione di riferimento dell’API di assegnazione tag.
* `TagManager` - consente di risolvere e creare tag in base a percorsi e nomi.
* `Tag` - definisce l&#39;oggetto tag.

### Ottenere un TagManager basato su JCR {#getting-a-jcr-based-tagmanager}

Per recuperare un&#39;istanza TagManager, è necessario disporre di un JCR `Session` e chiamare `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

Nel contesto Sling tipico, puoi anche adattarti a `TagManager` da `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recupero di un oggetto Tag {#retrieving-a-tag-object}

È possibile recuperare `Tag` tramite `TagManager`, risolvendo un tag esistente o creandone uno:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Per l&#39;implementazione basata su JCR, che mappa `Tags` su JCR `Nodes`, puoi utilizzare direttamente il meccanismo `adaptTo` di Sling se disponi della risorsa (ad esempio, `/content/cq:tags/default/my/tag`):

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
>L&#39;adattamento diretto da `Node` a `Tag` non è possibile perché `Node` non implementa il metodo Sling `Adaptable.adaptTo(Class)`.

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
>`RangeIterator` valido da utilizzare:
>
>`com.day.cq.commons.RangeIterator`

### Eliminazione dei tag {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replica dei tag {#replicating-tags}

È possibile utilizzare il servizio di replica ( `Replicator`) con i tag perché i tag sono di tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Assegnazione di tag sul lato client {#tagging-on-the-client-side}

Il widget del modulo `CQ.tagging.TagInputField` è per l&#39;immissione di tag. Dispone di un menu a comparsa per selezionare da tag esistenti, include il completamento automatico e molte altre funzioni. Il relativo xtype è `tags`.

## Tag Garbage Collector {#the-tag-garbage-collector}

Il garbage collector dei tag è un servizio in background che consente di pulire i tag nascosti e non utilizzati. I tag nascosti e inutilizzati sono tag al di sotto di `/content/cq:tags` che hanno una proprietà `cq:movedTo` e non sono utilizzati in un nodo di contenuto. Il conteggio è pari a zero. Utilizzando questo processo di eliminazione lenta, non è necessario aggiornare il nodo del contenuto (ovvero la proprietà `cq:tags`) come parte dell&#39;operazione di spostamento o unione. I riferimenti nella proprietà `cq:tags` vengono aggiornati automaticamente quando la proprietà `cq:tags` viene aggiornata, ad esempio tramite la finestra di dialogo delle proprietà della pagina.

Il garbage collector dei tag viene eseguito per impostazione predefinita una volta al giorno. Puoi configurarlo in:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Ricerca di tag ed elenco di tag {#tag-search-and-tag-listing}

La ricerca dei tag e l’elenco dei tag funzionano come segue:

* La ricerca di TagID cerca i tag la cui proprietà `cq:movedTo` è impostata su TagID e segue i `cq:movedTo` TagID.

* La ricerca del titolo del tag consente di cercare solo i tag che non hanno una proprietà `cq:movedTo`.

## Tag in lingue diverse {#tags-in-different-languages}

Come descritto nella documentazione per l&#39;amministrazione dei tag, nella sezione [Gestione dei tag in lingue diverse](/help/sites-administering/tags.md#managing-tags-in-different-languages) è possibile definire un tag `title` in lingue diverse. Al nodo del tag viene quindi aggiunta una proprietà sensibile alla lingua. Questa proprietà ha il formato `jcr:title.<locale>`, ad esempio `jcr:title.fr` per la traduzione francese. `<locale>` deve essere una stringa internazionale ISO minuscola e utilizzare &quot;_&quot; invece di &quot;-&quot;, ad esempio: `de_ch`.

Quando il tag **Animals** viene aggiunto alla pagina **Products**, il valore `stockphotography:animals` viene aggiunto alla proprietà `cq:tags` del nodo /content/geometrixx/en/products/jcr:content. Viene fatto riferimento alla traduzione dal nodo del tag.

L&#39;API lato server ha localizzato `title` metodi correlati:

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

`currentPage` e `slingRequest` sono disponibili in una JSP tramite il tag [&lt;cq:definedObjects>](/help/sites-developing/taglib.md).

Per i tag, la localizzazione dipende dal contesto, in quanto il tag `titles` può essere visualizzato nella lingua della pagina, nella lingua dell&#39;utente o in qualsiasi altra lingua.

### Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag {#adding-a-new-language-to-the-edit-tag-dialog}

Nella procedura seguente viene descritto come aggiungere una lingua (finlandese) alla finestra di dialogo **Modifica tag**:

1. In **CRXDE**, modificare la proprietà multivalore `languages` del nodo `/content/cq:tags`.

1. Aggiungere `fi_fi`, che rappresenta la lingua finlandese, e salvare le modifiche.

La nuova lingua (finlandese) è ora disponibile nella finestra di dialogo dei tag delle proprietà della pagina e nella finestra di dialogo **Modifica tag** quando si modifica un tag nella console **Assegnazione tag**.

>[!NOTE]
>
>La nuova lingua deve essere una delle lingue riconosciute dall&#39;AEM. Deve quindi essere disponibile come nodo sotto `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>L&#39;installazione del contenuto predefinito relativo ai tag tramite un pacchetto di aggiornamento ufficiale (inclusi Service Pack, Security Service Pack, Extended Feature Pack, Cumulative Feature Pack, patch e simili) reimposta la proprietà Languages del nodo `/content/cq:tags` sui valori predefiniti. Pertanto, è necessario aggiungerlo dalle proprietà prima dell’installazione.
