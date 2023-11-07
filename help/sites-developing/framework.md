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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%

---


# Framework di assegnazione tag AEM {#aem-tagging-framework}

L’assegnazione tag consente di categorizzare e organizzare i contenuti. I tag possono essere classificati in base a uno spazio dei nomi e a una tassonomia. Per informazioni dettagliate sull’utilizzo dei tag:

* Consulta il documento [Utilizzo dei tag](/help/sites-authoring/tags.md) per informazioni sull’assegnazione tag ai contenuti come autore di contenuti.
* Consulta il documento [Amministrazione dei tag](/help/sites-administering/tags.md) dal punto di vista di un amministratore, sulla creazione e la gestione dei tag e sulla modalità di applicazione dei tag di contenuto.

Questo articolo si concentra sul framework sottostante che supporta l’assegnazione tag in AEM e su come utilizzarlo come sviluppatore.

## Introduzione {#introduction}

Per assegnare tag ai contenuti e utilizzare l’infrastruttura di tag AEM:

* Il tag deve esistere come nodo di tipo `[cq:Tag](#tags-cq-tag-node-type)` sotto [nodo principale della tassonomia.](#taxonomy-root-node)

* Del nodo del contenuto con tag `NodeType` deve includere [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* Il [`TagID`](#tagid) viene aggiunto al nodo del contenuto [`cq:tags`](#tagged-content-cq-tags-property) e viene risolto in un nodo di tipo ` [cq:Tag](#tags-cq-tag-node-type)`.

## Tag : cq:Tag Node Type  {#tags-cq-tag-node-type}

La dichiarazione di un tag viene acquisita nell’archivio in un nodo di tipo `cq:Tag`.

Un tag può essere una parola semplice (ad esempio, `sky`) o rappresentano una tassonomia gerarchica (ad esempio,, `fruit/apple`, ovvero entrambi i generici `fruit` e le più specifiche `apple`).

I tag sono identificati da un TagID univoco.

Un tag include metadati facoltativi, ad esempio un titolo, titoli localizzati e una descrizione. Se presente, il titolo deve essere visualizzato nelle interfacce utente invece che nell’ID tag.

Il framework dei tag consente inoltre di limitare l’uso di specifici tag predefiniti da parte di autori e visitatori del sito.

### Caratteristiche tag {#tag-characteristics}

* Il tipo di nodo è `cq:Tag`n
* Il nome del nodo è un componente di [TagID](#tagid).
* Il [TagID](#tagid) include sempre un [spazio dei nomi.](#tag-namespace)
* Il `jcr:title` (il titolo da visualizzare nell’interfaccia utente) è facoltativo.
* Il `jcr:description` proprietà è facoltativa.
* Quando contiene nodi secondari, il tag viene indicato come [tag contenitore.](#container-tags)
* Il tag viene memorizzato nell’archivio sotto un percorso di base denominato [nodo principale della tassonomia.](#taxonomy-root-node)

Poiché i tag sono semplicemente nodi JCR, i nomi dei nodi devono rispettare il [Convenzione di denominazione JCR.](naming-conventions.md)

### ID tag {#tagid}

Un TagID identifica un percorso che viene risolto in un nodo di tag nell’archivio.

In genere, TagID è un TagID abbreviato che inizia con lo spazio dei nomi oppure può essere un TagID assoluto che inizia da [nodo principale della tassonomia.](#taxonomy-root-node)

Quando il contenuto viene taggato, se non esiste ancora, il `[cq:tags](#tagged-content-cq-tags-property)` viene aggiunta al nodo del contenuto e il TagID viene aggiunto al file `String` valore dell’array.

TagID è costituito da un tag [namespace](#tag-namespace) seguito dal valore TagID locale. [Tag contenitore](#container-tags) dispongono di tag secondari che rappresentano un ordine gerarchico nella tassonomia. I tag secondari possono essere utilizzati per fare riferimento ai tag come qualsiasi TagID locale. Ad esempio, l’assegnazione di tag al contenuto con `fruit` è consentito, anche se si tratta di un tag contenitore con tag secondari, come `fruit/apple` e `fruit/banana`.

### Nodo principale tassonomia {#taxonomy-root-node}

Il nodo principale della tassonomia è il percorso di base per tutti i tag nell’archivio. Il nodo principale della tassonomia non deve essere un nodo di tipo `cq:Tag`.

Nell’AEM, il percorso di base è `/content/cq:tags` e il nodo principale è di tipo `cq:Folder`.

### Spazio dei nomi dei tag {#tag-namespace}

Gli spazi dei nomi consentono di raggruppare gli elementi. Il caso d’uso più tipico è uno spazio dei nomi per sito (ad esempio, pubblico, interno e portale) o per applicazione più grande (ad esempio, WCM, Assets, Communities). Tuttavia, gli spazi dei nomi possono essere utilizzati per varie altre esigenze. Nell’interfaccia utente, gli spazi dei nomi vengono utilizzati solo per mostrare il sottoinsieme di tag (ad esempio, tag di un determinato spazio dei nomi) applicabile al contenuto corrente.

Lo spazio dei nomi del tag è il primo livello della sottostruttura della tassonomia, che è il nodo immediatamente sotto il [nodo principale tassonomia](#taxonomy-root-node). Uno spazio dei nomi è un nodo di tipo `cq:Tag` il cui elemento padre non è un `cq:Tag` tipo di nodo.

Tutti i tag hanno uno spazio dei nomi. Se non viene specificato alcuno spazio dei nomi, il tag viene assegnato allo spazio dei nomi predefinito, ovvero TagID `default` con il titolo `Standard Tags`, ovvero `/content/cq:tags/default`.

### Tag contenitore {#container-tags}

Un tag contenitore è un nodo di tipo `cq:Tag` contenente qualsiasi numero e tipo di nodi secondari, che consente di migliorare il modello di tag con metadati personalizzati.

Inoltre, i tag contenitore (o super tag) in una tassonomia fungono da sottotag di tutti i tag. Ad esempio, contenuto con tag `fruit/apple` è considerato come contrassegnato con `fruit` anche. In altre parole, la ricerca di contenuto con tag `fruit` troverebbe anche il contenuto taggato con `fruit/apple`.

### Risoluzione di TagID {#resolving-tagids}

Se TagID contiene due punti (`:`), i due punti separano lo spazio dei nomi dal tag o dalla tassonomia secondaria, che viene ulteriormente separata con barre (`/`). Se l’ID tag non ha due punti, viene implicito lo spazio dei nomi predefinito.

Di seguito è riportata la posizione standard e unica dei tag `/content/cq:tags`.

Tag che fa riferimento a percorsi non esistenti o che non puntano a un `cq:Tag` I nodi sono considerati non validi e vengono ignorati.

Nella tabella seguente vengono illustrati alcuni TagID di esempio, i relativi elementi e il modo in cui TagID viene risolto in un percorso assoluto nel repository:

| ID tag | Namespace | ID locale | Tag contenitore | Tag foglia | Percorso tag assoluto dell’archivio |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`, `apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | Nessuno | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | Nessuno | Nessuno | Nessuno, lo spazio dei nomi | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### Localizzazione del titolo del tag {#localization-of-tag-title}

Quando il tag include la stringa opzionale del titolo ( `jcr:title`), è possibile localizzare il titolo da visualizzare aggiungendo la proprietà `jcr:title.<locale>`.

Per ulteriori informazioni, consulta i seguenti documenti:

* [Tag in lingue diverse](/help/sites-developing/building.md#tags-in-different-languages), che descrive l’utilizzo delle API di
* [Gestione dei tag in lingue diverse](/help/sites-administering/tags.md#managing-tags-in-different-languages), che descrive l’utilizzo della console di assegnazione tag

### Controllo accesso {#access-control}

I tag esistono come nodi nell’archivio sotto [nodo principale tassonomia](#taxonomy-root-node). È possibile consentire o negare agli autori e ai visitatori del sito la creazione di tag in un determinato spazio dei nomi impostando ACL appropriati nell’archivio.

Inoltre, il rifiuto delle autorizzazioni di lettura per alcuni tag o spazi dei nomi controlla la possibilità di applicare tag a contenuto specifico.

Una pratica tipica include:

* Consentire `tag-administrators` accesso in scrittura gruppo/ruolo a tutti gli spazi dei nomi (aggiungi/modifica in `/content/cq:tags`). Questo gruppo viene fornito con AEM preconfigurato.
* Consente agli utenti/autori di accedere in lettura a tutti i namespace che dovrebbero essere leggibili (per lo più tutti).
* Consentire agli utenti/autori di accedere in scrittura agli spazi dei nomi in cui i tag devono essere liberamente definibili da parte di utenti/autori (aggiungere un nodo sotto `/content/cq:tags/some_namespace`)

## Contenuto assegnabile : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Per consentire agli sviluppatori di applicazioni di associare i tag a un tipo di contenuto, la registrazione del nodo ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) deve includere `cq:Taggable` mixin o `cq:OwnerTaggable` mixin.

Il `cq:OwnerTaggable` mixin, che eredita da `cq:Taggable`, ha lo scopo di indicare che il contenuto può essere classificato dal proprietario/autore. Nel AEM, è solo un attributo del `cq:PageContent` nodo. Il `cq:OwnerTaggable` Il mixin non è richiesto dal framework di assegnazione tag.

>[!NOTE]
>
>Si consiglia di abilitare i tag solo nel nodo di livello superiore di un elemento di contenuto aggregato (o nel relativo `jcr:content` nodo ). Alcuni esempi:
>
>* Pagine (`cq:Page`) in cui `jcr:content`il nodo è di tipo `cq:PageContent` che include `cq:Taggable` mixin
>* Risorse ( `cq:Asset`) in cui `jcr:content/metadata` il nodo ha sempre `cq:Taggable` mixin
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

Il `cq:tags` la proprietà è un `String` array utilizzato per memorizzare uno o più TagID quando vengono applicati al contenuto da autori o visitatori del sito. La proprietà ha un significato solo quando viene aggiunta a un nodo definito con `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>Per utilizzare la funzionalità di assegnazione tag AEM, le applicazioni sviluppate personalizzate non devono definire proprietà di tag diverse da `cq:tags`.

## Spostamento e unione di tag {#moving-and-merging-tags}

Di seguito è riportata una descrizione degli effetti nell&#39;archivio durante lo spostamento o l&#39;unione di tag utilizzando [console di assegnazione tag](/help/sites-administering/tags.md):

* Quando un tag A viene spostato o unito al tag B in `/content/cq:tags`:

   * Il tag A non viene eliminato e ottiene un `cq:movedTo` proprietà.
   * Il tag B viene creato (in caso di spostamento) e ottiene un `cq:backlinks` proprietà.

* `cq:movedTo` punta al tag B.

   * Questa proprietà indica che il tag A è stato spostato o unito al tag B. Se si sposta il tag B, la proprietà viene aggiornata di conseguenza. Il tag A è quindi nascosto ed è mantenuto solo nell’archivio per risolvere gli ID tag nei nodi di contenuto che puntano al tag A. Il garbage collector dei tag rimuove tag come tag A una volta che nessun altro nodo di contenuto vi punta.

   * Un valore speciale per `cq:movedTo` la proprietà è `nirvana`. Viene applicato quando il tag viene eliminato, ma non può essere rimosso dall’archivio perché sono presenti tag secondari con `cq:movedTo` questo deve essere mantenuto.

  >[!NOTE]
  >
  >Il `cq:movedTo` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
  >
  >1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento) o
  >1. Il tag include elementi figlio già spostati.

* `cq:backlinks` mantiene i riferimenti nella direzione opposta. In altre parole, mantiene un elenco di tutti i tag che sono stati spostati o uniti con il tag B. Questo è principalmente necessario per mantenere `cq:movedTo` proprietà aggiornate quando il tag B viene anche spostato/unito/eliminato o quando il tag B viene attivato, nel qual caso devono essere attivati anche tutti i relativi tag di backlink.

  >[!NOTE]
  >
  >Il `cq:backlinks` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
  >
  >1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento) OPPURE
  >1. Il tag include elementi figlio già spostati.

* Lettura di un `cq:tags` La proprietà di un nodo di contenuto prevede la seguente risoluzione:

   1. Se non viene trovata alcuna corrispondenza in `/content/cq:tags`, non viene restituito alcun tag.

   1. Se il tag ha `cq:movedTo` impostata, viene seguito l’ID tag di riferimento.

      * Questo passaggio viene ripetuto purché il tag seguito abbia `cq:movedTo` proprietà.

   1. Se il tag seguito non ha un `cq:movedTo` , il tag viene letto.

* Per pubblicare la modifica quando un tag è stato spostato o unito, la `cq:Tag` e tutti i relativi backlink devono essere replicati. Questa operazione viene eseguita automaticamente quando il tag viene attivato nella console di amministrazione dei tag.

* Aggiornamenti successivi al `cq:tags` pulisci automaticamente i riferimenti precedenti. Questo viene attivato perché la risoluzione di un tag spostato tramite l’API restituisce il tag di destinazione, fornendo così l’ID del tag di destinazione.

>[!NOTE]
>
>Lo spostamento dei tag è diverso dalla migrazione dei tag.

## Migrazione tag {#tags-migration}

A partire da Adobe Experience Manager 6.4, i tag vengono memorizzati in `/content/cq:tags` mentre le versioni precedenti memorizzavano i tag in `/etc/tags`.

Ogni volta che si aggiorna un sistema AEM da una versione precedente alla 6.4, è necessario migrare i tag a `/content/cq:tags`. Consulta [Ristrutturazione dell’archivio comune in AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags) per ulteriori informazioni.
