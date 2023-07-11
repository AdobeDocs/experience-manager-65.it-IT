---
title: Framework di assegnazione tag AEM
description: Assegnare tag ai contenuti e utilizzare l’infrastruttura di tag AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# Framework di assegnazione tag AEM {#aem-tagging-framework}

Per assegnare tag ai contenuti e utilizzare l&#39;infrastruttura dei tag AEM:

* Il tag deve esistere come nodo di tipo ` [cq:Tag](#tags-cq-tag-node-type)` sotto [nodo principale tassonomia](#taxonomy-root-node)

* Il NodeType del nodo di contenuto con tag deve includere [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* Il [TagID](#tagid) viene aggiunto al nodo del contenuto [`cq:tags`](#tagged-content-cq-tags-property) e viene risolto in un nodo di tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Tag : cq:Tag Node Type  {#tags-cq-tag-node-type}

La dichiarazione di un tag viene acquisita nell’archivio in un nodo di tipo `cq:Tag.`

Un tag può essere una parola semplice (ad esempio, cielo) o rappresentare una tassonomia gerarchica (ad esempio, frutta/mela, che significa sia il frutto generico che la mela più specifica).

I tag sono identificati da un TagID univoco.

Un tag include metadati facoltativi, ad esempio un titolo, titoli localizzati e una descrizione. Se presente, il titolo deve essere visualizzato nelle interfacce utente invece che nell’ID tag.

Il framework dei tag consente inoltre di limitare l’uso di specifici tag predefiniti da parte di autori e visitatori del sito.

### Caratteristiche tag {#tag-characteristics}

* il tipo di nodo è `cq:Tag`
* il nome del nodo è un componente di ` [TagID](#tagid)`
* il ` [TagID](#tagid)` include sempre un [namespace](#tag-namespace)

* facoltativo `jcr:title` (il Titolo da visualizzare nell’interfaccia utente)

* facoltativo `jcr:description` proprietà

* quando si contengono nodi secondari, viene indicato come [tag contenitore](#container-tags)
* viene memorizzato nel repository sotto un percorso di base denominato [nodo principale tassonomia](#taxonomy-root-node)

### ID tag {#tagid}

Un TagID identifica un percorso che viene risolto in un nodo di tag nell’archivio.

In genere, TagID è un TagID abbreviato che inizia con lo spazio dei nomi oppure può essere un TagID assoluto che inizia da [nodo principale tassonomia](#taxonomy-root-node).

Quando il contenuto viene taggato, se non esiste ancora, il ` [cq:tags](#tagged-content-cq-tags-property)` viene aggiunta al nodo del contenuto e TagID al valore della matrice String della proprietà.

TagID è costituito da un tag [namespace](#tag-namespace) seguito dal valore TagID locale. [Tag contenitore](#container-tags) dispongono di tag secondari che rappresentano un ordine gerarchico nella tassonomia. I tag secondari possono essere utilizzati per fare riferimento ai tag come qualsiasi TagID locale. Ad esempio, è consentito assegnare tag al contenuto con &quot;frutta&quot;, anche se si tratta di un tag contenitore con sottocartelle quali &quot;frutta/mela&quot; e &quot;frutta/banana&quot;.

### Nodo principale tassonomia {#taxonomy-root-node}

Il nodo principale della tassonomia è il percorso di base per tutti i tag nell’archivio. Il nodo principale della tassonomia deve *non* essere un nodo di tipo `  cq   :Tag`.

Nell’AEM, il percorso di base è `/content/  cq   :tags` e il nodo principale è di tipo `  cq   :Folder`.

### Spazio dei nomi dei tag {#tag-namespace}

Gli spazi dei nomi consentono di raggruppare gli elementi. Il caso d’uso più tipico consiste nell’avere uno spazio dei nomi per sito (web) (ad esempio pubblico, interno e portale) o per applicazione più grande (ad esempio, WCM, Assets, Communities), ma gli spazi dei nomi possono essere utilizzati per varie altre esigenze. Gli spazi dei nomi vengono utilizzati nell’interfaccia utente per mostrare solo il sottoinsieme di tag (ovvero i tag di un determinato spazio dei nomi) applicabile al contenuto corrente.

Lo spazio dei nomi del tag è il primo livello della sottostruttura della tassonomia, che è il nodo immediatamente sotto il [nodo principale tassonomia](#taxonomy-root-node). Uno spazio dei nomi è un nodo di tipo `cq:Tag` il cui elemento padre non è un `cq:Tag`tipo di nodo.

Tutti i tag hanno uno spazio dei nomi. Se non viene specificato alcuno spazio dei nomi, il tag viene assegnato allo spazio dei nomi predefinito, ovvero TagID `default` (Il titolo è `Standard Tags),`che è `/content/cq:tags/default.`

### Tag contenitore {#container-tags}

Un tag contenitore è un nodo di tipo `cq:Tag` contenente qualsiasi numero e tipo di nodi secondari, che consente di migliorare il modello di tag con metadati personalizzati.

Inoltre, i tag contenitore (o super-tag) in una tassonomia fungono da sommatoria di tutti i tag secondari. Ad esempio, il contenuto taggato con frutta/mela è considerato taggato anche con frutta. In altre parole, la ricerca di contenuti taggati con frutta troverebbe anche i contenuti taggati con frutta/mela.

### Risoluzione di TagID {#resolving-tagids}

Se l’ID del tag contiene i due punti &quot;:&quot;, il due punti separa lo spazio dei nomi dal tag o dalla tassonomia secondaria, che vengono quindi separati con le normali barre &quot;/&quot;. Se l’ID tag non ha due punti, viene implicito lo spazio dei nomi predefinito.

La posizione standard e unica dei tag è inferiore a /content/cq:tags.

I tag che fanno riferimento a percorsi non esistenti o che non puntano a un nodo cq:Tag vengono considerati non validi e vengono ignorati.

Nella tabella seguente vengono illustrati alcuni TagID di esempio, i relativi elementi e il modo in cui TagID viene risolto in un percorso assoluto nel repository:

Nella tabella seguente vengono illustrati alcuni TagID di esempio, i relativi elementi e il modo in cui TagID viene risolto in un percorso assoluto nel repository:

<table>
 <tbody>
  <tr>
   <td><strong>ID tag<br /> </strong></td>
   <td><strong>Namespace</strong></td>
   <td><strong>ID locale</strong></td>
   <td><strong>Tag contenitore</strong></td>
   <td><strong>Tag foglia</strong></td>
   <td><strong>Archivio<br /> Percorso tag assoluto</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braeburn</td>
   <td>dam</td>
   <td>frutta/mela/braeburn</td>
   <td>frutta, mela</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>colore/rosso</td>
   <td>impostazione predefinita</td>
   <td>colore/rosso</td>
   <td>colore</td>
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
   <td>(nessuno, lo spazio dei nomi)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>categoria</td>
   <td>automobile</td>
   <td>automobile</td>
   <td>automobile</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### Localizzazione del titolo del tag {#localization-of-tag-title}

Quando il tag include la stringa opzionale del titolo ( `jcr:title`) è possibile localizzare il titolo da visualizzare aggiungendo la proprietà `jcr:title.<locale>`.

Per ulteriori dettagli, consulta

* [Tag in lingue diverse](/help/sites-developing/building.md#tags-in-different-languages) - che descrive l’utilizzo delle API
* [Gestione dei tag in lingue diverse](/help/sites-administering/tags.md#managing-tags-in-different-languages) - che descrive l’utilizzo della console Tag

### Controllo accesso {#access-control}

I tag esistono come nodi nell’archivio sotto [nodo principale tassonomia](#taxonomy-root-node). È possibile consentire o negare agli autori e ai visitatori del sito la creazione di tag in un determinato spazio dei nomi impostando ACL appropriati nell’archivio.

Inoltre, il rifiuto delle autorizzazioni di lettura per alcuni tag o spazi dei nomi controlla la possibilità di applicare i tag a contenuto specifico.

Una pratica tipica include:

* Consentire `tag-administrators` accesso in scrittura gruppo/ruolo a tutti gli spazi dei nomi (aggiungi/modifica in `/content/cq:tags`). Questo gruppo viene fornito con AEM preconfigurato.

* Consente agli utenti/autori di accedere in lettura a tutti i namespace che dovrebbero essere leggibili (per lo più tutti).
* Consentire a utenti/autori di accedere in scrittura agli spazi dei nomi in cui i tag devono essere liberamente definibili da utenti/autori (add_node in `/content/cq:tags/some_namespace`)

## Contenuto assegnabile : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Per consentire agli sviluppatori di applicazioni di associare i tag a un tipo di contenuto, la registrazione del nodo ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) deve includere `cq:Taggable` mixin o `cq:OwnerTaggable` mixin.

Il `cq:OwnerTaggable` mixin, che eredita da `cq:Taggable`, ha lo scopo di indicare che il contenuto può essere classificato dal proprietario/autore. Nel AEM, è solo un attributo del `cq:PageContent` nodo. Il `cq:OwnerTaggable` Il mixin non è richiesto dal framework di assegnazione tag.

>[!NOTE]
>
>Si consiglia di abilitare i tag solo nel nodo di livello superiore di un elemento di contenuto aggregato (o nel relativo nodo jcr:content). Alcuni esempi:
>
>* pagine ( `cq:Page`) in cui `jcr:content`il nodo è di tipo `cq:PageContent` che include `cq:Taggable` mixin.
>
>* risorse ( `cq:Asset`) in cui `jcr:content/metadata` il nodo ha sempre `cq:Taggable` mixin.
>

### Notazione del tipo di nodo (CND) {#node-type-notation-cnd}

Le definizioni dei tipi di nodo esistono nell’archivio come file CND. La notazione CND è definita come parte della documentazione JCR [qui](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Le definizioni essenziali per i tipi di nodo inclusi nell’AEM sono le seguenti:

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

Il `cq:tags` La proprietà è una matrice di stringhe utilizzata per memorizzare uno o più TagID quando vengono applicati al contenuto da autori o visitatori del sito. La proprietà ha un significato solo quando viene aggiunta a un nodo definito con `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>Per utilizzare la funzionalità di assegnazione tag AEM, le applicazioni sviluppate personalizzate non devono definire proprietà di tag diverse da `cq:tags`.

## Spostamento e unione di tag {#moving-and-merging-tags}

Di seguito è riportata una descrizione degli effetti nell&#39;archivio durante lo spostamento o l&#39;unione di tag utilizzando [Console assegnazione tag](/help/sites-administering/tags.md):

* Quando un tag A viene spostato o unito al tag B in `/content/cq:tags`:

   * il tag A non viene eliminato e ottiene un `cq:movedTo` proprietà.
   * viene creato il tag B (se si è verificato uno spostamento) e ottiene un `cq:backlinks` proprietà.

* `cq:movedTo` punta al tag B. Questa proprietà indica che il tag A è stato spostato o unito al tag B. Se si sposta il tag B, la proprietà viene aggiornata di conseguenza. Il tag A è quindi nascosto ed è mantenuto solo nell’archivio per risolvere gli ID tag nei nodi di contenuto che puntano al tag A. Il garbage collector dei tag rimuove tag come tag A una volta che nessun altro nodo di contenuto vi punta.
Un valore speciale per `cq:movedTo` la proprietà è `nirvana`: viene applicata quando il tag viene eliminato, ma non può essere rimossa dall’archivio perché sono presenti tag secondari con `cq:movedTo` questo deve essere mantenuto.

  >[!NOTE]
  >
  >Il `cq:movedTo` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
  >
  >1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento) OPPURE
  >1. Il tag include elementi figlio già spostati.

* `cq:backlinks` mantiene i riferimenti nella direzione opposta. In altre parole, mantiene un elenco di tutti i tag che sono stati spostati o uniti con il tag B. Questo è principalmente necessario per mantenere `cq:movedTo`proprietà aggiornate quando il tag B viene anche spostato/unito/eliminato o quando il tag B viene attivato, nel qual caso devono essere attivati anche tutti i relativi tag di backlink.

  >[!NOTE]
  >
  >Il `cq:backlinks` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
  >
  >1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento) OPPURE
  >1. Il tag include elementi figlio già spostati.

* Lettura di un `cq:tags` La proprietà di un nodo di contenuto prevede la seguente risoluzione:

   1. Se non viene trovata alcuna corrispondenza in `/content/cq:tags`, non viene restituito alcun tag.
   1. Se il tag ha `cq:movedTo` impostata, viene seguito l’ID tag di riferimento.
Questo passaggio viene ripetuto purché il tag seguito abbia `cq:movedTo` proprietà.

   1. Se il tag seguito non ha un `cq:movedTo` , il tag viene letto.

* Per pubblicare la modifica quando un tag è stato spostato o unito, la `cq:Tag` deve essere replicato il nodo e tutti i relativi collegamenti precedenti: questa operazione viene eseguita automaticamente quando il tag viene attivato nella console di amministrazione dei tag.

* Aggiornamenti successivi al `cq:tags` pulisci automaticamente i riferimenti &quot;vecchi&quot;. Questo viene attivato perché la risoluzione di un tag spostato tramite l’API restituisce il tag di destinazione, fornendo così l’ID del tag di destinazione.

>[!NOTE]
>
>Lo spostamento dei tag è diverso dalla migrazione dei tag.

## Migrazione dei tag {#tags-migration}

a partire dall&#39;Experience Manager 6.4 i tag sono memorizzati in `/content/cq:tags`, precedentemente archiviati in `/etc/tags`. Tuttavia, negli scenari in cui Adobe Experience Manager è stato aggiornato dalla versione precedente, i tag sono ancora presenti nella posizione precedente `/etc/tags`. Nei sistemi aggiornati, è necessario eseguire la migrazione dei tag in `/content/cq:tags`.

>[!NOTE]
>
>Nella pagina Proprietà pagina dei tag, si consiglia di utilizzare l’ID tag (`geometrixx-outdoors:activity/biking`) invece di utilizzare l’hard coding del percorso base del tag (ad esempio, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Per elencare i tag: `com.day.cq.tagging.servlets.TagListServlet` possono essere utilizzati.

>[!NOTE]
>
>È consigliabile utilizzare l’API di gestione tag come risorsa.

### Se l’istanza AEM aggiornata supporta l’API TagManager {#upgraded-instance-support-tagmanager-api}

1. All’inizio del componente, l’API TagManager rileva se si tratta di un’istanza AEM aggiornata. Nel sistema aggiornato, i tag sono memorizzati in `/etc/tags`.

1. L’API TagManager viene quindi eseguita in modalità di compatibilità con le versioni precedenti, il che significa che utilizza `/etc/tags` come percorso di base. In caso contrario, utilizza una nuova posizione `/content/cq:tags`.

1. Aggiorna la posizione dei tag.

1. Dopo aver trasferito i tag nella nuova posizione, esegui il seguente script:

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

Lo script recupera tutti i tag che hanno `/etc/tags` nel valore di `cq:movedTo/cq:backLinks` proprietà. Quindi scorre il set di risultati recuperato e risolve il `cq:movedTo` e `cq:backlinks` valori proprietà a `/content/cq:tags` percorsi (se `/etc/tags` viene rilevato nel valore).

### Se l’istanza AEM aggiornata viene eseguita nell’interfaccia classica {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>L’interfaccia classica non è compatibile con il downtime pari a zero e non supporta il nuovo percorso di base dei tag. Se desideri utilizzare l’interfaccia classica, `/etc/tags` deve essere creato e seguito da `cq-tagging` riavvio del componente.

Se nell’interfaccia classica sono presenti istanze AEM aggiornate supportate dall’API TagManager ed in esecuzione:

1. Una volta fa riferimento al percorso base del tag precedente `/etc/tags` vengono sostituiti utilizzando tagId o una nuova posizione tag `/content/cq:tags`, è possibile migrare i tag nella nuova posizione `/content/cq:tags` in CRX seguito dal riavvio del componente.

1. Dopo aver trasferito i tag nella nuova posizione, esegui lo script indicato sopra.
