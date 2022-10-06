---
title: Creazione di tag in un’applicazione AEM
seo-title: Building Tagging into an AEM Application
description: Funzionamento programmatico con tag o estensione tag all'interno di un'applicazione AEM personalizzata
seo-description: Programmatically work with tags or extending tags within a custom AEM application
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# Creazione di tag in un’applicazione AEM{#building-tagging-into-an-aem-application}

Per lavorare in modo programmatico con i tag o estendere i tag all&#39;interno di un&#39;applicazione di AEM personalizzata, questa pagina descrive l&#39;utilizzo del

* [API di assegnazione tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

che interagisce con

* [Framework di assegnazione tag](/help/sites-developing/framework.md)

Per informazioni correlate sull’assegnazione tag, consulta :

* [Amministrazione dei tag](/help/sites-administering/tags.md) per informazioni sulla creazione e la gestione dei tag e sui tag di contenuto applicati.
* [Utilizzo dei tag](/help/sites-authoring/tags.md) per informazioni sull’assegnazione tag al contenuto.

## Panoramica dell’API di assegnazione tag {#overview-of-the-tagging-api}

L&#39;attuazione [framework di assegnazione tag](/help/sites-developing/framework.md) in AEM consente la gestione di tag e contenuti tag utilizzando l’ API JCR . TagManager assicura che i tag immessi come valori nel `cq:tags` la proprietà string array non è duplicata, rimuove gli ID tag che puntano a tag non esistenti e aggiorna gli ID tag per i tag spostati o uniti. TagManager utilizza un listener di osservazione JCR che ripristina eventuali modifiche errate. Le classi principali sono [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) pacchetto:

* JcrTagManagerFactory - restituisce un&#39;implementazione basata su JCR di un `TagManager`. È l’implementazione di riferimento dell’API di assegnazione tag.
* `TagManager` - consente di risolvere e creare tag in base a percorsi e nomi.
* `Tag` - definisce l’oggetto tag .

### Ottenere un TagManager basato su JCR {#getting-a-jcr-based-tagmanager}

Per recuperare un’istanza TagManager, è necessario disporre di un JCR `Session` e di chiamare `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

Nel contesto Sling tipico puoi anche adattarti a un `TagManager` dal `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recupero di un oggetto Tag {#retrieving-a-tag-object}

A `Tag` può essere recuperato tramite `TagManager`, risolvendo un tag esistente o creandone uno nuovo:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Per l’implementazione basata su JCR, che mappa `Tags` su JCR `Nodes`, puoi utilizzare direttamente gli `adaptTo` se disponi della risorsa (ad esempio `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Mentre un tag può essere convertito solo *da *una risorsa (non un nodo), un tag può essere convertito *sia in un nodo che in una risorsa :

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adattamento diretto da `Node` a `Tag` non è possibile, perché `Node` non implementa Sling `Adaptable.adaptTo(Class)` metodo .

### Ottenimento e impostazione dei tag {#getting-and-setting-tags}

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
>Il valore valido `RangeIterator` da utilizzare:
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

## Assegnazione tag sul lato client {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` è un widget modulo per l’immissione di tag. Dispone di un menu a comparsa per la selezione tra i tag esistenti, include il completamento automatico e molte altre funzioni. Il suo xtype è `tags`.

## Tag Garbage Collector {#the-tag-garbage-collector}

Il tag garbage Collector è un servizio di background che pulisce i tag nascosti e inutilizzati. I tag nascosti e non utilizzati sono tag sottostanti `/content/cq:tags` che hanno `cq:movedTo` e non vengono utilizzati su un nodo di contenuto - hanno un conteggio di zero. Utilizzando questo processo di eliminazione pigra, il nodo del contenuto (ovvero `cq:tags` non è necessario aggiornare come parte dell&#39;operazione di spostamento o unione. I riferimenti nel `cq:tags` viene automaticamente aggiornata quando `cq:tags` viene aggiornata, ad esempio tramite la finestra di dialogo delle proprietà della pagina.

Il Garbage Collector dei tag viene eseguito per impostazione predefinita una volta al giorno. Puoi configurarlo in:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Ricerca tag ed elenco tag {#tag-search-and-tag-listing}

La ricerca di tag e l’elenco dei tag funzionano come segue:

* La ricerca di TagID cerca i tag che hanno la proprietà `cq:movedTo` impostato su TagID e segue `cq:movedTo` TagIDs.

* La ricerca per il titolo del tag cerca solo i tag che non hanno un `cq:movedTo` proprietà.

## Tag in diverse lingue {#tags-in-different-languages}

Come descritto nella documentazione per l’amministrazione dei tag, nella sezione [Gestione dei tag in diverse lingue](/help/sites-administering/tags.md#managing-tags-in-different-languages), un tag `title`può essere definito in lingue diverse. Al nodo del tag viene quindi aggiunta una proprietà sensibile alla lingua. Questa proprietà ha il formato `jcr:title.<locale>`ad esempio `jcr:title.fr` per la traduzione francese. `<locale>` deve essere una stringa internazionale ISO in minuscolo e utilizzare &quot;_&quot; invece di &quot;-&quot;, ad esempio: `de_ch`.

Quando il **Animali** viene aggiunto al **Prodotti** page, il valore `stockphotography:animals` viene aggiunto alla proprietà `cq:tags` del nodo /content/geometrixx/en/products/jcr:content. La traduzione viene referenziata dal nodo del tag.

L’API lato server è localizzata `title`Metodi correlati:

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Impostazioni internazionali)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Impostazioni internazionali)
   * getTitlePath(Impostazioni internazionali)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, locale)
   * createTagByTitle(Stringa tagTitlePath, Impostazioni internazionali)
   * resolveByTitle(String tagTitlePath, locale)

In AEM, la lingua può essere ottenuta dalla lingua della pagina o dalla lingua dell’utente:

* per recuperare la lingua della pagina in un JSP:

   * `currentPage.getLanguage(false)`

* per recuperare la lingua utente in un JSP:

   * `slingRequest.getLocale()`

`currentPage` e `slingRequest` sono disponibili in un JSP attraverso [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) tag .

Per l’assegnazione tag, la localizzazione dipende dal contesto come tag `titles`può essere visualizzato nella lingua della pagina, nella lingua dell’utente o in qualsiasi altra lingua.

### Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag {#adding-a-new-language-to-the-edit-tag-dialog}

La procedura seguente descrive come aggiungere una nuova lingua (finlandese) al **Modifica tag** finestra di dialogo:

1. In **CRXDE**, modifica la proprietà multivalore `languages` del nodo `/content/cq:tags`.

1. Aggiungi `fi_fi` - che rappresenta le impostazioni internazionali finlandesi e salva le modifiche.

La nuova lingua (finlandese) è ora disponibile nella finestra di dialogo dei tag delle proprietà della pagina e nella **Modifica tag** durante la modifica di un tag **Assegnazione tag** console.

>[!NOTE]
>
>La nuova lingua deve essere una delle lingue riconosciute AEM, cioè deve essere disponibile come nodo qui sotto `/libs/wcm/core/resources/languages`.
