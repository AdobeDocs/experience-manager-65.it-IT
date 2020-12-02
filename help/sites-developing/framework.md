---
title: AEM Tagging Framework
seo-title: AEM Tagging Framework
description: Assegnare tag ai contenuti e sfruttare l’infrastruttura di tag AEM
seo-description: Assegnare tag ai contenuti e sfruttare l’infrastruttura di tag AEM
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 0%

---


# AEM Framework di assegnazione tag {#aem-tagging-framework}

Per assegnare tag ai contenuti e sfruttare l&#39;infrastruttura di tag AEM:

* Il tag deve essere presente come nodo di tipo ` [cq:Tag](#tags-cq-tag-node-type)` sotto il nodo principale [tassonomia](#taxonomy-root-node)

* NodeType del nodo del contenuto con tag deve includere il mixin [ `cq:Taggable`](#taggable-content-cq-taggable-mixin)
* Il tag [ID](#tagid) viene aggiunto alla proprietà [ `cq:tags`](#tagged-content-cq-tags-property) del nodo di contenuto e viene risolto in un nodo di tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Tag: cq:Tag Node Type {#tags-cq-tag-node-type}

La dichiarazione di un tag viene acquisita nella directory archivio in un nodo di tipo `cq:Tag.`

Un tag può essere una parola semplice (ad es. cielo) o rappresentare una tassonomia gerarchica (ad es. frutta/mela, che significa sia il frutto generico che la mela più specifica).

I tag sono identificati da un ID tag univoco.

Un tag contiene metadati facoltativi quali un titolo, titoli localizzati e una descrizione. Se presente, il titolo deve essere visualizzato nelle interfacce utente anziché in TagID.

Il framework di assegnazione tag consente inoltre di limitare gli autori e i visitatori del sito a utilizzare solo tag predefiniti specifici.

### Caratteristiche del tag {#tag-characteristics}

* il tipo di nodo è `cq:Tag`
* il nome del nodo è un componente di ` [TagID](#tagid)`
* la ` [TagID](#tagid)` include sempre [spazio dei nomi](#tag-namespace)

* proprietà opzionale `jcr:title` (il Titolo da visualizzare nell&#39;interfaccia utente)

* proprietà opzionale `jcr:description`

* quando contiene nodi secondari, è denominato [tag contenitore](#container-tags)
* è memorizzato nell&#39;archivio sotto un percorso di base denominato [nodo radice tassonomia](#taxonomy-root-node)

### ID tag {#tagid}

Un TagID identifica un percorso che risolve un nodo di tag nell&#39;archivio.

In genere, il TagID è un TagID abbreviato che inizia con lo spazio dei nomi o può essere un TagID assoluto a partire dal nodo radice [tassonomia](#taxonomy-root-node).

Quando un contenuto è dotato di tag, se non esiste ancora, la proprietà ` [cq:tags](#tagged-content-cq-tags-property)` viene aggiunta al nodo del contenuto e il tagID viene aggiunto al valore dell&#39;array String della proprietà.

Il TagID è composto da [namespace](#tag-namespace) seguito dall&#39;identificatore TagID locale. [I ](#container-tags) tag contenitore contengono tag secondari che rappresentano un ordine gerarchico nella tassonomia. I tag secondari possono essere utilizzati per fare riferimento ai tag come qualsiasi ID tag locale. Ad esempio, è consentito aggiungere tag &quot;frutta&quot; al contenuto, anche se si tratta di un tag contenitore con tag secondari, quali &quot;frutta/mela&quot; e &quot;frutta/banana&quot;.

### Nodo radice tassonomia {#taxonomy-root-node}

Il nodo principale della tassonomia è il percorso di base per tutti i tag presenti nella directory archivio. Il nodo radice tassonomia deve essere *not* un nodo di tipo `  cq   :Tag`.

In AEM, il percorso di base è `/content/  cq   :tags` e il nodo principale è di tipo `  cq   :Folder`.

### Tag Namespace {#tag-namespace}

Gli spazi dei nomi consentono di raggruppare gli elementi. Il caso d’uso più tipico consiste nell’avere uno spazio nomi per sito (Web) (ad esempio pubblico, interno e portale) o per applicazione più grande (ad esempio WCM, Risorse, Community), ma gli spazi dei nomi possono essere utilizzati per varie altre esigenze. Gli spazi dei nomi vengono utilizzati nell&#39;interfaccia utente per mostrare solo il sottoinsieme di tag (cioè i tag di un determinato spazio dei nomi) applicabile al contenuto corrente.

Lo spazio dei nomi del tag è il primo livello nella struttura ad albero secondaria della tassonomia, ovvero il nodo immediatamente sotto il nodo radice [tassonomia](#taxonomy-root-node). Uno spazio dei nomi è un nodo di tipo `cq:Tag` il cui elemento principale non è un tipo di nodo `cq:Tag`.

Tutti i tag hanno uno spazio nomi. Se non viene specificato alcuno spazio dei nomi, il tag viene assegnato allo spazio dei nomi predefinito, che è TagID `default` (il titolo è `Standard Tags),`ovvero `/content/cq:tags/default.`

### Tag contenitore {#container-tags}

Un tag contenitore è un nodo di tipo `cq:Tag` contenente qualsiasi numero e tipo di nodi secondari, che consente di migliorare il modello di tag con metadati personalizzati.

Inoltre, i tag contenitore (o super-tag) in una tassonomia fungono da sottotitoli per tutti i tag secondari: ad esempio, il contenuto etichettato con frutta/mela è considerato anche etichettato con frutta, cioè la ricerca di contenuti semplicemente etichettati con frutta troverebbe anche il contenuto etichettato con frutta/mela.

### Risoluzione di ID tag {#resolving-tagids}

Se l&#39;ID del tag contiene due punti &quot;:&quot;, i due punti separano lo spazio dei nomi dal tag o dalla sotto-tassonomia, che vengono quindi separati con le normali barre &quot;/&quot;. Se l&#39;ID del tag non ha due punti, lo spazio dei nomi predefinito è implicito.

La posizione standard e unica dei tag si trova sotto /content/cq:tags.

I tag che fanno riferimento a percorsi o percorsi non esistenti che non puntano a un nodo cq:Tag vengono considerati non validi e vengono ignorati.

Nella tabella seguente sono riportati alcuni tag ID di esempio, i relativi elementi e il modo in cui il tagID corrisponde a un percorso assoluto nell’archivio:

Nella tabella seguente sono riportati alcuni tag ID di esempio, i relativi elementi e il modo in cui il tagID corrisponde a un percorso assoluto nell’archivio:
Nella tabella seguente sono riportati alcuni tag ID di esempio, i relativi elementi e il modo in cui il tagID corrisponde a un percorso assoluto nell’archivio:

<table>
 <tbody>
  <tr>
   <td><strong>ID tag<br /> </strong></td>
   <td><strong>Namespace</strong></td>
   <td><strong>ID locale</strong></td>
   <td><strong>Tag contenitore</strong></td>
   <td><strong>Tag foglia</strong></td>
   <td><strong>Percorso tag assoluto del repository<br /></strong></td>
  </tr>
  <tr>
   <td>diga:frutta/mela/rombo</td>
   <td>dam</td>
   <td>frutta/mela/rombo</td>
   <td>frutta, mela</td>
   <td>burrone</td>
   <td>/content/cq:tags/dam/apple/braeburn</td>
  </tr>
  <tr>
   <td>color/red</td>
   <td>impostazione predefinita</td>
   <td>color/red</td>
   <td>color</td>
   <td>rosso</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>cielo</td>
   <td>impostazione predefinita</td>
   <td>cielo</td>
   <td>(nessuno)</td>
   <td>cielo</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>dam</td>
   <td>(nessuno)</td>
   <td>(nessuno)</td>
   <td>(none, lo spazio dei nomi)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>category</td>
   <td>auto</td>
   <td>auto</td>
   <td>auto</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### Localizzazione del titolo del tag {#localization-of-tag-title}

Se il tag include la stringa titolo opzionale ( `jcr:title`), è possibile localizzare il titolo per la visualizzazione aggiungendo la proprietà `jcr:title.<locale>`.

Per maggiori dettagli vedi

* [Tag in diverse lingue](/help/sites-developing/building.md#tags-in-different-languages) , che descrive l&#39;utilizzo delle API
* [Gestione dei tag in diverse lingue](/help/sites-administering/tags.md#managing-tags-in-different-languages) , che descrive l’utilizzo della console Assegnazione tag

### Controllo accesso {#access-control}

I tag esistono come nodi nel repository sotto il nodo principale [tassonomia](#taxonomy-root-node). È possibile consentire o negare agli autori e ai visitatori del sito di creare tag in un dato spazio nomi impostando ACL appropriati nell&#39;archivio.

Inoltre, negare le autorizzazioni di lettura per alcuni tag o spazi di nomi controllerà la possibilità di applicare tag a contenuti specifici.

Una pratica tipica include:

* Consentire a `tag-administrators` gruppo/ruolo di accedere in scrittura a tutti gli spazi dei nomi (aggiungere/modificare in `/content/cq:tags`). Questo gruppo viene fornito con AEM out-of-the-box.

* Consentire a utenti/autori di accedere in lettura a tutti gli spazi dei nomi che dovrebbero essere leggibili (per lo più tutti).
* Consentire a utenti/autori di accedere in scrittura agli spazi di nomi in cui i tag devono essere liberamente definibili da utenti/autori (add_node in `/content/cq:tags/some_namespace`)

## Contenuto variabile: cq:Mixin variabile {#taggable-content-cq-taggable-mixin}

Affinché gli sviluppatori di applicazioni possano allegare tag a un tipo di contenuto, la registrazione del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) deve includere il mixin `cq:Taggable` o il mixin `cq:OwnerTaggable`.

Il mixin `cq:OwnerTaggable`, che eredita da `cq:Taggable`, ha lo scopo di indicare che il contenuto può essere classificato dal proprietario/autore. In AEM, è solo un attributo del nodo `cq:PageContent`. Il mixin `cq:OwnerTaggable` non è richiesto dal framework di assegnazione tag.

>[!NOTE]
>
>Si consiglia di abilitare solo i tag sul nodo di primo livello di un elemento di contenuto aggregato (o sul relativo nodo jcr:content). Alcuni esempi:
>
>* pagine ( `cq:Page`) in cui il nodo `jcr:content`è di tipo `cq:PageContent` che include il mixin `cq:Taggable`.
   >
   >
* risorse ( `cq:Asset`) in cui il nodo `jcr:content/metadata` ha sempre il mixin `cq:Taggable`.

>



### Notazione del tipo di nodo (CND) {#node-type-notation-cnd}

Le definizioni dei tipi di nodo esistono nell&#39;archivio come file CND. La notazione CND è definita come parte della documentazione JCR [qui](https://jackrabbit.apache.org/node-type-notation.html).

Le definizioni essenziali per i tipi di nodo inclusi in AEM sono le seguenti:

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## Contenuto con tag: cq:tags, proprietà {#tagged-content-cq-tags-property}

La proprietà `cq:tags` è un array String utilizzato per memorizzare uno o più ID di tag quando vengono applicati al contenuto da autori o visitatori del sito. La proprietà ha significato solo se aggiunta a un nodo definito con il mixin `[cq:Taggable](#taggable-content-cq-taggable-mixin)`.

>[!NOTE]
>
>Per sfruttare AEM funzionalità di tag, le applicazioni sviluppate personalizzate non devono definire proprietà di tag diverse da `cq:tags`.

## Spostamento e unione dei tag {#moving-and-merging-tags}

Di seguito è riportata una descrizione degli effetti presenti nell&#39;archivio durante lo spostamento o l&#39;unione dei tag mediante la [console Tagging](/help/sites-administering/tags.md):

* Quando un tag A viene spostato o unito nel tag B in `/content/cq:tags`:

   * il tag A non viene eliminato e ottiene una proprietà `cq:movedTo`.
   * il tag B viene creato (nel caso di uno spostamento) e ottiene una proprietà `cq:backlinks`.

* `cq:movedTo` punta al tag B. Questa proprietà indica che il tag A è stato spostato o unito nel tag B. Se si sposta il tag B, questa proprietà verrà aggiornata di conseguenza. Il tag A è quindi nascosto e viene conservato solo nell’archivio per risolvere gli ID tag nei nodi di contenuto che puntano al tag A. Il raccoglitore di tag per elementi indesiderati rimuove i tag come tag A, a cui nessun altro nodo di contenuto punta.
Un valore speciale per la proprietà `cq:movedTo` è `nirvana`: viene applicato quando il tag viene eliminato ma non può essere rimosso dalla directory archivio perché esistono tag secondari con un elemento `cq:movedTo` che deve essere mantenuto.

   >[!NOTE]
   >
   >La proprietà `cq:movedTo` viene aggiunta al tag spostato o unito solo se è soddisfatta una delle seguenti condizioni:
   > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento) O
   > 1. Nel tag sono presenti elementi figlio che sono già stati spostati.


* `cq:backlinks` mantiene i riferimenti nella direzione opposta, ossia tiene un elenco di tutti i tag spostati o uniti al tag B. Questa funzione è principalmente necessaria per mantenere  `cq:movedTo`le proprietà aggiornate quando il tag B viene spostato/unito/eliminato o quando il tag B viene attivato, nel qual caso tutti i tag backlink devono essere attivati.

   >[!NOTE]
   >
   >La proprietà `cq:backlinks` viene aggiunta al tag spostato o unito solo se è soddisfatta una delle seguenti condizioni:
   >
   > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento) O    >
   > 1. Nel tag sono presenti elementi figlio che sono già stati spostati.


* La lettura di una proprietà `cq:tags` di un nodo di contenuto comporta la seguente risoluzione:

   1. Se non è presente alcuna corrispondenza in `/content/cq:tags`, non viene restituito alcun tag.
   1. Se il tag ha una proprietà `cq:movedTo` impostata, viene seguito l&#39;ID del tag di riferimento.
Questo passaggio viene ripetuto purché il tag seguito abbia una proprietà `cq:movedTo`.

   1. Se il tag seguito non ha una proprietà `cq:movedTo`, il tag viene letto.

* Per pubblicare la modifica quando un tag è stato spostato o unito, è necessario replicare il nodo `cq:Tag` e tutti i relativi backlink: questa operazione viene eseguita automaticamente quando il tag viene attivato nella console di amministrazione dei tag.

* Gli aggiornamenti successivi alla proprietà `cq:tags` della pagina puliscono automaticamente i riferimenti &quot;vecchi&quot;. Questo viene attivato perché la risoluzione di un tag spostato attraverso l&#39;API restituisce il tag di destinazione, fornendo così l&#39;ID del tag di destinazione.

>[!NOTE]
>
>Il movimento dei tag è diverso dalla migrazione dei tag.

## Migrazione tag {#tags-migration}

 Experience Manager 6.4 in poi i tag sono memorizzati in `/content/cq:tags`, precedentemente memorizzati in `/etc/tags`. Tuttavia, negli scenari in cui Adobe Experience Manager è stato aggiornato dalla versione precedente, i tag sono ancora presenti nella vecchia posizione `/etc/tags`. Nei sistemi aggiornati i tag devono essere migrati in `/content/cq:tags`.

>[!NOTE]
>
>Nella pagina Proprietà pagina dei tag si consiglia di utilizzare l&#39;ID tag (`geometrixx-outdoors:activity/biking`) invece di codificare il percorso base del tag (ad esempio, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Per elencare i tag, è possibile utilizzare `com.day.cq.tagging.servlets.TagListServlet`.

>[!NOTE]
>
>Si consiglia di utilizzare l&#39;API di gestione tag come risorsa.

### Se AEM&#39;istanza aggiornata supporta l&#39;API TagManager {#upgraded-instance-support-tagmanager-api}

1. All’inizio del componente, l’API TagManager rileva se si tratta di un’istanza AEM aggiornata. Nel sistema aggiornato, i tag sono memorizzati in `/etc/tags`.

1. L&#39;API TagManager viene quindi eseguita in modalità di compatibilità con versioni precedenti, il che significa che l&#39;API utilizza `/etc/tags` come percorso di base. In caso contrario, utilizza la nuova posizione `/content/cq:tags`.

1. Aggiorna il percorso dei tag.

1. Dopo aver migrato i tag nella nuova posizione, eseguire lo script seguente:

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

Lo script raccoglie tutti i tag con `/etc/tags` nel valore della proprietà `cq:movedTo/cq:backLinks`. Viene quindi ripetuto il set di risultati ottenuto e i valori delle proprietà `cq:movedTo` e `cq:backlinks` vengono risolti nei percorsi `/content/cq:tags` (nel caso in cui `/etc/tags` venga rilevato nel valore).

### Se l&#39;istanza AEM aggiornata viene eseguita nell&#39;interfaccia classica {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>L&#39;interfaccia classica non è conforme allo zero tempi di inattività e non supporta il nuovo percorso della base tag. Per utilizzare l&#39;interfaccia classica, è necessario creare un componente diverso da `/etc/tags` seguito dal riavvio del componente `cq-tagging`.

In caso di istanze AEM aggiornate supportate dall&#39;API TagManager e in esecuzione nell&#39;interfaccia classica:

1. Una volta sostituiti i riferimenti al vecchio percorso base tag `/etc/tags` con tagId o alla nuova posizione tag `/content/cq:tags`, potete migrare i tag nella nuova posizione `/content/cq:tags` in CRX seguita dal riavvio del componente.

1. Dopo aver trasferito i tag nella nuova posizione, eseguire lo script di cui sopra.
