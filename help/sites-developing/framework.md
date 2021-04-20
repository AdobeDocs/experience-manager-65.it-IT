---
title: Framework di assegnazione tag AEM
seo-title: Framework di assegnazione tag AEM
description: Assegnare tag ai contenuti e sfruttare l’infrastruttura di assegnazione tag AEM
seo-description: Assegnare tag ai contenuti e sfruttare l’infrastruttura di assegnazione tag AEM
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# Framework di assegnazione tag AEM {#aem-tagging-framework}

Per assegnare tag ai contenuti e sfruttare l’infrastruttura di assegnazione tag AEM :

* Il tag deve esistere come nodo di tipo ` [cq:Tag](#tags-cq-tag-node-type)` sotto il nodo principale [tassonomia](#taxonomy-root-node)

* NodeType del nodo del contenuto con tag deve includere il mixin [ `cq:Taggable`](#taggable-content-cq-taggable-mixin)
* Il tag [TagID](#tagid) viene aggiunto alla proprietà [ `cq:tags`](#tagged-content-cq-tags-property) del nodo di contenuto e viene risolto in un nodo di tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Tag : cq:Tag Node Type {#tags-cq-tag-node-type}

La dichiarazione di un tag viene acquisita nell’archivio in un nodo di tipo `cq:Tag.`

Un tag può essere una parola semplice (ad esempio cielo) o rappresentare una tassonomia gerarchica (ad esempio frutta/mela, che significa sia il frutto generico che la mela più specifica).

I tag sono identificati da un TagID univoco.

Un tag contiene metadati facoltativi, ad esempio un titolo, titoli localizzati e una descrizione. Il titolo deve essere visualizzato nelle interfacce utente invece del tagID, se presente.

Il framework di assegnazione tag consente inoltre di limitare gli autori e i visitatori del sito a utilizzare solo tag predefiniti specifici.

### Caratteristiche del tag {#tag-characteristics}

* il tipo di nodo è `cq:Tag`
* il nome del nodo è un componente del` [TagID](#tagid)`
* il ` [TagID](#tagid)` include sempre un [namespace](#tag-namespace)

* proprietà opzionale `jcr:title` (titolo da visualizzare nell’interfaccia utente)

* proprietà opzionale `jcr:description`

* quando contiene nodi figlio, è indicato come [tag contenitore](#container-tags)
* è memorizzato nell&#39;archivio sotto un percorso di base denominato [nodo principale della tassonomia](#taxonomy-root-node)

### ID tag {#tagid}

Un TagID identifica un percorso che viene risolto in un nodo di tag nell&#39;archivio.

In genere, il TagID è un TagID abbreviato che inizia con lo spazio dei nomi o può essere un TagID assoluto a partire dal [nodo principale della tassonomia](#taxonomy-root-node).

Quando il contenuto è taggato, se non esiste ancora, la proprietà ` [cq:tags](#tagged-content-cq-tags-property)` viene aggiunta al nodo del contenuto e il TagID viene aggiunto al valore dell&#39;array String della proprietà.

Il TagID è costituito da un [namespace](#tag-namespace) seguito dal TagID locale. [I tag ](#container-tags) contenitore consentono di usare tag secondari che rappresentano un ordine gerarchico nella tassonomia. I tag secondari possono essere utilizzati per fare riferimento ai tag come qualsiasi altro TagID locale. Ad esempio, è consentita l’assegnazione di tag al contenuto con &quot;frutta&quot;, anche se si tratta di un tag contenitore con tag secondari, come &quot;frutta/mela&quot; e &quot;frutta/banana&quot;.

### Nodo principale tassonomia {#taxonomy-root-node}

Il nodo principale della tassonomia è il percorso di base per tutti i tag nel repository. Il nodo principale della tassonomia deve essere *not* un nodo di tipo `  cq   :Tag`.

In AEM, il percorso di base è `/content/  cq   :tags` e il nodo principale è di tipo `  cq   :Folder`.

### Tag Namespace {#tag-namespace}

I namespace consentono di raggruppare gli elementi. Il caso d’uso più tipico è quello di avere uno spazio dei nomi per sito (web) (ad esempio pubblico, interno e portale) o per applicazione più grande (ad esempio WCM, Assets, Communities), ma i namespace possono essere utilizzati per varie altre esigenze. I namespace vengono utilizzati nell’interfaccia utente per mostrare solo il sottoinsieme di tag (ovvero i tag di un determinato namespace) applicabile al contenuto corrente.

Lo spazio dei nomi del tag è il primo livello della struttura secondaria della tassonomia, che è il nodo immediatamente sotto il nodo principale [tassonomia](#taxonomy-root-node). Uno spazio dei nomi è un nodo di tipo `cq:Tag` il cui elemento padre non è un tipo di nodo `cq:Tag`.

Tutti i tag hanno uno spazio dei nomi. Se non viene specificato alcun namespace, il tag viene assegnato allo spazio dei nomi predefinito, che è TagID `default` (il titolo è `Standard Tags),`ovvero `/content/cq:tags/default.`

### Tag contenitore {#container-tags}

Un tag contenitore è un nodo di tipo `cq:Tag` contenente qualsiasi numero e tipo di nodi secondari, che consente di migliorare il modello di tag con metadati personalizzati.

Inoltre, i tag contenitore (o super tag) in una tassonomia fungono da sotto-somma di tutti i tag secondari: ad esempio, il contenuto contrassegnato con frutta/mela è considerato anche marcato con frutta, cioè la ricerca di contenuto semplicemente marcato con frutta trova anche il contenuto marcato con frutta/mela.

### Risoluzione degli ID tag {#resolving-tagids}

Se l’ID del tag contiene due punti &quot;:&quot;, il due punti separa lo spazio dei nomi dal tag o dalla tassonomia secondaria, che vengono quindi separati con le normali barre &quot;/&quot;. Se l’ID del tag non ha due punti, viene implicito il namespace predefinito.

La posizione standard e unica dei tag è sotto /content/cq:tags.

I tag che fanno riferimento a percorsi o percorsi non esistenti che non puntano a un nodo cq:Tag sono considerati non validi e vengono ignorati.

La tabella seguente mostra alcuni tagID di esempio, i relativi elementi e il modo in cui il tagID viene risolto in un percorso assoluto nell’archivio:

La tabella seguente mostra alcuni tagID di esempio, i relativi elementi e il modo in cui il tagID viene risolto in un percorso assoluto nell’archivio :
La tabella seguente mostra alcuni tagID di esempio, i relativi elementi e il modo in cui il tagID viene risolto in un percorso assoluto nell’archivio :

<table>
 <tbody>
  <tr>
   <td><strong>ID tag<br /> </strong></td>
   <td><strong>Namespace</strong></td>
   <td><strong>ID locale</strong></td>
   <td><strong>Tag contenitore</strong></td>
   <td><strong>Tag foglia</strong></td>
   <td><strong>Repository<br /> Percorso tag assoluto</strong></td>
  </tr>
  <tr>
   <td>dam:frutta/mela/braeburn</td>
   <td>diga</td>
   <td>frutta/mela/cervello</td>
   <td>frutta, mela</td>
   <td>burrasca</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>colore/rosso</td>
   <td>impostazione predefinita</td>
   <td>colore/rosso</td>
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
   <td>diga</td>
   <td>(nessuno)</td>
   <td>(nessuno)</td>
   <td>(Nessuno, spazio dei nomi)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>categoria</td>
   <td>auto</td>
   <td>auto</td>
   <td>auto</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### Localizzazione del titolo del tag {#localization-of-tag-title}

Quando il tag include la stringa del titolo opzionale ( `jcr:title`), è possibile localizzare il titolo da visualizzare aggiungendo la proprietà `jcr:title.<locale>`.

Per ulteriori dettagli vedi

* [Tag in diverse lingue](/help/sites-developing/building.md#tags-in-different-languages)  - che descrive l’utilizzo delle API
* [Gestione dei tag in diverse lingue](/help/sites-administering/tags.md#managing-tags-in-different-languages)  - che descrive l’utilizzo della console Tagging

### Controllo accesso {#access-control}

I tag esistono come nodi nell&#39;archivio sotto il nodo principale [tassonomia](#taxonomy-root-node). È possibile consentire o negare agli autori e ai visitatori del sito di creare tag in un dato spazio dei nomi impostando ACL appropriati nell’archivio.

Inoltre, negare le autorizzazioni di lettura per alcuni tag o namespace controllerà la possibilità di applicare tag a contenuti specifici.

Una pratica tipica include:

* Consentire a `tag-administrators` gruppo/ruolo di accedere in scrittura a tutti i namespace (aggiungere/modificare in `/content/cq:tags`). Questo gruppo viene fornito con AEM preconfigurato.

* Consentire agli utenti/autori di accedere in lettura a tutti i namespace che dovrebbero essere leggibili per loro (per lo più tutti).
* Consentire a utenti/autori di accedere in scrittura a quei namespace in cui i tag devono essere liberamente definibili da utenti/autori (aggiungi_nodo sotto `/content/cq:tags/some_namespace`)

## Contenuto variabile : cq:Mixin taggabile {#taggable-content-cq-taggable-mixin}

Affinché gli sviluppatori di applicazioni possano allegare tag a un tipo di contenuto, la registrazione del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) deve includere il mixin `cq:Taggable` o il mixin `cq:OwnerTaggable`.

Il mixin `cq:OwnerTaggable`, che eredita da `cq:Taggable`, ha lo scopo di indicare che il contenuto può essere classificato dal proprietario/autore. In AEM, è solo un attributo del nodo `cq:PageContent`. Il mixin `cq:OwnerTaggable` non è richiesto dal framework di assegnazione tag.

>[!NOTE]
>
>Si consiglia di abilitare solo i tag sul nodo di primo livello di un elemento di contenuto aggregato (o sul relativo nodo jcr:content). Gli esempi includono:
>
>* pagine ( `cq:Page`) in cui il nodo `jcr:content`è di tipo `cq:PageContent` che include il mixin `cq:Taggable`.
   >
   >
* risorse ( `cq:Asset`) dove il nodo `jcr:content/metadata` ha sempre il mixin `cq:Taggable`.

>



### Notazione del tipo di nodo (CND) {#node-type-notation-cnd}

Le definizioni dei tipi di nodo esistono nell’archivio come file CND. La notazione CND è definita come parte della documentazione JCR [qui](https://jackrabbit.apache.org/node-type-notation.html).

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

## Contenuto con tag: cq:tags Property {#tagged-content-cq-tags-property}

La proprietà `cq:tags` è una matrice String utilizzata per memorizzare uno o più TagID applicati al contenuto da autori o visitatori del sito. La proprietà ha un significato solo quando viene aggiunta a un nodo definito con il mixin `[cq:Taggable](#taggable-content-cq-taggable-mixin)`.

>[!NOTE]
>
>Per sfruttare AEM funzionalità di assegnazione tag, le applicazioni sviluppate personalizzate non devono definire proprietà di tag diverse da `cq:tags`.

## Spostamento e unione dei tag {#moving-and-merging-tags}

Di seguito è riportata una descrizione degli effetti nell’archivio durante lo spostamento o l’unione dei tag utilizzando la [console Tagging](/help/sites-administering/tags.md):

* Quando un tag A viene spostato o unito nel tag B in `/content/cq:tags`:

   * Il tag A non viene eliminato e ottiene una proprietà `cq:movedTo` .
   * Il tag B viene creato (in caso di spostamento) e ottiene una proprietà `cq:backlinks` .

* `cq:movedTo` fa riferimento al tag B. Questa proprietà significa che il tag A è stato spostato o unito nel tag B. Lo spostamento del tag B comporterà l’aggiornamento di questa proprietà di conseguenza. Il tag A è quindi nascosto e viene mantenuto nell’archivio solo per risolvere gli ID tag nei nodi di contenuto che puntano al tag A. Il tag garbage Collector rimuove i tag come il tag A una volta nessun altro nodo di contenuto li punta.
Un valore speciale per la proprietà `cq:movedTo` è `nirvana`: viene applicato quando il tag viene eliminato ma non può essere rimosso dall’archivio perché sono presenti tag secondari con un `cq:movedTo` che devono essere mantenuti.

   >[!NOTE]
   >
   >La proprietà `cq:movedTo` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
   > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento) O
   > 1. Il tag include elementi secondari già spostati.


* `cq:backlinks` mantiene i riferimenti nell’altra direzione, ovvero mantiene un elenco di tutti i tag spostati o uniti con il tag B. Questo è richiesto principalmente per mantenere  `cq:movedTo`le proprietà aggiornate quando il tag B viene spostato/unito/eliminato o quando il tag B viene attivato, nel qual caso devono essere attivati anche tutti i suoi backlink.

   >[!NOTE]
   >
   >La proprietà `cq:backlinks` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
   >
   > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento) O    >
   > 1. Il tag include elementi secondari già spostati.


* La lettura di una proprietà `cq:tags` di un nodo di contenuto comporta la seguente risoluzione:

   1. Se non esiste alcuna corrispondenza sotto `/content/cq:tags`, non viene restituito alcun tag.
   1. Se per il tag è impostata una proprietà `cq:movedTo` , viene seguito l&#39;ID del tag di riferimento.
Questo passaggio viene ripetuto purché il tag seguito abbia una proprietà `cq:movedTo` .

   1. Se il tag seguito non ha una proprietà `cq:movedTo` , viene letto il tag .

* Per pubblicare la modifica quando un tag è stato spostato o unito, è necessario replicare il nodo `cq:Tag` e tutti i relativi backlink: questa operazione viene eseguita automaticamente quando il tag viene attivato nella console di amministrazione dei tag.

* Successivamente, gli aggiornamenti alla proprietà `cq:tags` della pagina puliscono automaticamente i riferimenti &quot;vecchi&quot;. Questo viene attivato perché la risoluzione di un tag spostato attraverso l&#39;API restituisce il tag di destinazione, fornendo così l&#39;ID del tag di destinazione.

>[!NOTE]
>
>Lo spostamento dei tag è diverso dalla migrazione dei tag.

## Migrazione dei tag {#tags-migration}

I tag di Experience Manager 6.4 e successivi sono memorizzati in `/content/cq:tags`, che erano precedentemente memorizzati in `/etc/tags`. Tuttavia, negli scenari in cui Adobe Experience Manager è stato aggiornato dalla versione precedente, i tag sono ancora presenti nella vecchia posizione `/etc/tags`. Nei sistemi aggiornati è necessario eseguire la migrazione dei tag in `/content/cq:tags`.

>[!NOTE]
>
>Nella pagina Proprietà pagina della pagina dei tag , è consigliabile utilizzare l’ID tag (`geometrixx-outdoors:activity/biking`) invece di codificare il percorso base del tag (ad esempio, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Per elencare i tag, è possibile utilizzare `com.day.cq.tagging.servlets.TagListServlet`.

>[!NOTE]
>
>È consigliabile utilizzare l’API di gestione tag come risorsa.

### Se l&#39;istanza AEM aggiornata supporta l&#39;API TagManager {#upgraded-instance-support-tagmanager-api}

1. All’inizio del componente, l’API TagManager rileva se si tratta di un’istanza AEM aggiornata. Nel sistema aggiornato, i tag vengono memorizzati in `/etc/tags`.

1. L’API TagManager viene quindi eseguita in modalità di retrocompatibilità, il che significa che l’API utilizza `/etc/tags` come percorso di base. In caso contrario, utilizza la nuova posizione `/content/cq:tags`.

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

Lo script recupera tutti i tag che hanno `/etc/tags` nel valore della proprietà `cq:movedTo/cq:backLinks` . Quindi esegue un&#39;iterazione del set di risultati recuperato e risolve i valori delle proprietà `cq:movedTo` e `cq:backlinks` in percorsi `/content/cq:tags` (nel caso in cui `/etc/tags` viene rilevato nel valore).

### Se l&#39;istanza AEM aggiornata viene eseguita nell&#39;interfaccia classica {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>L’interfaccia classica non è conforme allo zero tempi di inattività e non supporta il nuovo percorso di base dei tag. Per utilizzare l’interfaccia classica, è necessario creare `/etc/tags` e riavviare il componente `cq-tagging`.

In caso di istanze AEM aggiornate supportate dall&#39;API TagManager ed eseguite nell&#39;interfaccia classica:

1. Una volta sostituiti i riferimenti al vecchio percorso base tag `/etc/tags` utilizzando tagId o nuova posizione tag `/content/cq:tags`, puoi migrare i tag nella nuova posizione `/content/cq:tags` in CRX seguito dal riavvio del componente.

1. Dopo aver trasferito i tag nella nuova posizione, esegui lo script menzionato sopra.
