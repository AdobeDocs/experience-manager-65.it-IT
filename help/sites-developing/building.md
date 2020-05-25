---
title: Creazione di tag in un’applicazione AEM
seo-title: Creazione di tag in un’applicazione AEM
description: Gestione programmatica dei tag o estensione dei tag all'interno di un'applicazione AEM personalizzata
seo-description: Gestione programmatica dei tag o estensione dei tag all'interno di un'applicazione AEM personalizzata
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
translation-type: tm+mt
source-git-commit: 1493b301ecf4c25f785495e11ead352de600ddb7
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# Creazione di tag in un’applicazione AEM{#building-tagging-into-an-aem-application}

Per utilizzare in modo programmatico i tag o estenderli all’interno di un’applicazione AEM personalizzata, questa pagina descrive l’utilizzo del

* [API di tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

che interagisce con il

* [Framework di tag](/help/sites-developing/framework.md)

Per ulteriori informazioni sui tag, vedere:

* [Amministrazione dei tag](/help/sites-administering/tags.md) per informazioni sulla creazione e la gestione dei tag, nonché per l’applicazione dei tag di contenuto.
* [Utilizzo dei tag](/help/sites-authoring/tags.md) per informazioni sui tag nel contenuto.

## Panoramica dell’API Tagging {#overview-of-the-tagging-api}

L’implementazione del framework [di](/help/sites-developing/framework.md) tag in AEM consente di gestire tag e contenuti tag mediante l’API JCR. TagManager assicura che i tag immessi come valori nella proprietà dell&#39;array di `cq:tags` stringhe non vengano duplicati, rimuove gli ID di tag che puntano a tag non esistenti e aggiorna gli ID di tag per i tag spostati o uniti. TagManager utilizza un listener di osservazione JCR che ripristina le modifiche non corrette. Le classi principali si trovano nel pacchetto [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) :

* JcrTagManagerFactory - restituisce un&#39;implementazione JCR di un `TagManager`. È l’implementazione di riferimento dell’API Tagging.
* `TagManager` - consente di risolvere e creare tag in base a percorsi e nomi.
* `Tag` - definisce l&#39;oggetto tag.

### Ottenimento di un gestore di tag basato su JCR {#getting-a-jcr-based-tagmanager}

Per recuperare un’istanza TagManager, è necessario disporre di un JCR `Session` e chiamare `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

Nel tipico contesto Sling è anche possibile adattarsi a un `TagManager` da `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Ottenimento di un oggetto Tag {#retrieving-a-tag-object}

Un `Tag` può essere recuperato tramite `TagManager`, risolvendo un tag esistente o creandone uno nuovo:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Per l&#39;implementazione basata su JCR, che viene mappata `Tags` su JCR `Nodes`, potete utilizzare direttamente il `adaptTo` meccanismo di Sling se disponete della risorsa (ad esempio, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Mentre un tag può essere convertito solo *da *una risorsa (non un nodo), un tag può essere convertito *in *sia un nodo che una risorsa:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>L&#39;adattamento diretto da `Node` a `Tag` non è possibile, perché `Node` non implementa il `Adaptable.adaptTo(Class)` metodo Sling.

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
>La valida `RangeIterator` da utilizzare è:
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

`CQ.tagging.TagInputField` è un widget modulo per l’immissione di tag. Dispone di un menu a comparsa per la selezione tra i tag esistenti, include il completamento automatico e molte altre funzioni. Il suo xtype è `tags`.

## Tag Garbage Collector {#the-tag-garbage-collector}

Il Garbage Collector tag è un servizio di sfondo che pulisce i tag nascosti e inutilizzati. I tag nascosti e inutilizzati sono tag sottostanti `/content/cq:tags` che hanno una `cq:movedTo` proprietà e non vengono utilizzati su un nodo di contenuto; il conteggio è pari a zero. Utilizzando questo processo di eliminazione pigra, il nodo di contenuto (ovvero la `cq:tags` proprietà) non deve essere aggiornato come parte dell&#39;operazione di spostamento o unione. I riferimenti nella `cq:tags` proprietà vengono aggiornati automaticamente quando la `cq:tags` proprietà viene aggiornata, ad esempio tramite la finestra di dialogo delle proprietà della pagina.

Per impostazione predefinita, il Garbage Collector tag viene eseguito una volta al giorno. È possibile configurare in:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Ricerca tag ed Elenco tag {#tag-search-and-tag-listing}

La ricerca di tag e l’elenco dei tag funzionano come segue:

* La ricerca di TagID cerca i tag la cui proprietà è `cq:movedTo` impostata su TagID e segue gli `cq:movedTo` ID tag.

* La ricerca di Titolo tag cerca solo i tag privi di `cq:movedTo` proprietà.

## Tags in Different Languages {#tags-in-different-languages}

Come descritto nella documentazione relativa all’amministrazione dei tag, nella sezione [Gestione dei tag in lingue](/help/sites-administering/tags.md#managing-tags-in-different-languages)diverse `title`è possibile definire un tag in lingue diverse. Al nodo del tag viene quindi aggiunta una proprietà sensibile alla lingua. Questa proprietà ha il formato `jcr:title.<locale>`, ad esempio `jcr:title.fr` per la traduzione francese. `<locale>` Deve essere una stringa di lingua ISO in lettere minuscole e utilizzare &quot;_&quot; invece di &quot;-&quot;, ad esempio: `de_ch`.

Quando il tag **Animals** viene aggiunto alla pagina **Products** , il valore `stockphotography:animals` viene aggiunto alla proprietà `cq:tags` del nodo /content/geometrixx/en/products/jcr:content. Il nodo del tag fa riferimento alla traduzione.

L&#39;API lato server presenta metodi `title`correlati localizzati:

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Impostazioni internazionali)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Impostazioni internazionali)
   * getTitlePath(Impostazioni internazionali)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale)
   * createTagByTitle(String tagTitlePath, Locale)
   * resolveByTitle(String tagTitlePath, locale)

In AEM, la lingua può essere ottenuta dalla lingua della pagina o dalla lingua dell’utente:

* per recuperare la lingua della pagina in una JSP:

   * `currentPage.getLanguage(false)`

* per recuperare la lingua utente in una JSP:

   * `slingRequest.getLocale()`

`currentPage` e `slingRequest` sono disponibili in una JSP tramite il tag [&lt;cq:definedObjects>](/help/sites-developing/taglib.md) .

Per i tag, la localizzazione dipende dal contesto in cui i tag `titles`possono essere visualizzati nella lingua della pagina, nella lingua dell’utente o in qualsiasi altra lingua.

### Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag {#adding-a-new-language-to-the-edit-tag-dialog}

La procedura seguente descrive come aggiungere una nuova lingua (finlandese) alla finestra di dialogo Modifica **** tag:

1. In **CRXDE**, modificare la proprietà multivalore `languages` del nodo `/content/cq:tags`.

1. Aggiungete `fi_fi` - che rappresenta l&#39;impostazione internazionale finlandese - e salvate le modifiche.

La nuova lingua (finlandese) è ora disponibile nella finestra di dialogo dei tag delle proprietà della pagina e nella finestra di dialogo **Modifica tag** quando si modifica un tag nella console **Tag** .

>[!NOTE]
>
>La nuova lingua deve essere una delle lingue riconosciute da AEM, ovvero deve essere disponibile come nodo sottostante `/libs/wcm/core/resources/languages`.

