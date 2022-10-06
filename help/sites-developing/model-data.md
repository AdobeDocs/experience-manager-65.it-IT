---
title: Modellazione dei dati - Modello di David Nuescheler
seo-title: Data Modeling - David Nuescheler's Model
description: Raccomandazioni per la modellazione dei contenuti di David Nuescheler
seo-description: David Nuescheler's content modelling recommendations
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 0%

---

# Modellazione dei dati - Modello di David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Sorgente {#source}

I seguenti dettagli sono idee e commenti espressi da David Nuescheler.

David è stato co-fondatore e CTO of Day Software AG, uno dei principali fornitori di software per la gestione dei contenuti e l&#39;infrastruttura dei contenuti globali, richiesto dall&#39;Adobe nel 2010. È ora compagno e vicepresidente di Enterprise Technology all&#39;Adobe e guida anche lo sviluppo di JSR-170, l&#39;interfaccia API (Application Programming Interface) Java Content Repository, lo standard tecnologico per la gestione dei contenuti.

Ulteriori aggiornamenti sono disponibili su [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## Introduzione da David {#introduction-from-david}

In varie discussioni ho scoperto che gli sviluppatori sono in qualche modo a disagio con le funzioni e le funzionalità presentate da JCR per quanto riguarda la modellazione dei contenuti. Non esiste ancora una guida e poca esperienza su come modellare i contenuti in un archivio e sul perché un modello di contenuto è migliore dell’altro.

Mentre nel mondo relazionale l&#39;industria del software ha molta esperienza su come modellare i dati, siamo ancora alle prime fasi per lo spazio dell&#39;archivio dei contenuti.

Vorrei iniziare a riempire questo vuoto esprimendo le mie opinioni personali sul modo in cui i contenuti dovrebbero essere modellati, sperando che questo possa un giorno diventare qualcosa di più significativo per la comunità degli sviluppatori, che non è solo &quot;la mia opinione&quot;, ma qualcosa di più generale applicabile. Considerate questo il mio primo bersaglio veloce ed evoluto.

>[!NOTE]
>
>Disclaimer: Queste linee guida esprimono le mie opinioni personali, talvolta controverse. Sono ansioso di discutere questi orientamenti e di perfezionarli.

## Sette semplici regole {#seven-simple-rules}

### Regola n. 1: Prima i dati, poi la struttura. Forse. {#rule-data-first-structure-later-maybe}

#### Spiegazione {#explanation-1}

Consiglio di non preoccuparsi di una struttura dati dichiarata in senso ERD. Inizialmente.

Impara ad amare nt:unstructured (&amp; Friends) nello sviluppo.

Credo che Stefano lo riassuma più o meno.

La mia linea di fondo: La struttura è costosa e in molti casi non è assolutamente necessario dichiarare esplicitamente la struttura allo stoccaggio sottostante.

Esiste un contratto implicito sulla struttura che l&#39;applicazione utilizza in modo intrinseco. Supponiamo di memorizzare la data di modifica di un post di blog in una proprietà lastModified . La mia app saprà automaticamente leggere di nuovo la data di modifica da quella stessa proprietà, non c&#39;è davvero bisogno di dichiararlo esplicitamente.

Ulteriori vincoli relativi ai dati, come vincoli obbligatori o di tipo e di valore, dovrebbero essere applicati solo se richiesto per motivi di integrità dei dati.

#### Esempio {#example-1}

L’esempio precedente di utilizzo di un `lastModified` La proprietà Date, ad esempio il nodo &quot;post di blog&quot;, non significa in realtà che ci sia bisogno di un tipo di nodo speciale. Io userei sicuramente `nt:unstructured` almeno inizialmente per i nodi del post del mio blog. Dal momento che nella mia applicazione di blog tutto ciò che farò è mostrare la data dell&#39;ultima modifica comunque (possibilmente &quot;ordine entro&quot;) Mi importa a malapena se è un Data affatto. Dato che mi fido implicitamente della mia applicazione di scrittura di blog per mettere lì una &quot;data&quot; comunque, non c&#39;è davvero bisogno di dichiarare la presenza di un `lastModified` data sotto forma di nodetype a.

### Regola n. 2: Guidare la gerarchia dei contenuti, non lasciare che accada. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Spiegazione {#explanation-2}

La gerarchia dei contenuti è una risorsa molto preziosa. Quindi non lasciate che accada, progettatela. Se non avete un nome &quot;buono&quot; e leggibile per un nodo, probabilmente è qualcosa che dovreste riconsiderare. I numeri arbitrari non sono mai un &quot;buon nome&quot;.

Anche se può essere estremamente facile mettere rapidamente un modello relazionale esistente in un modello gerarchico, si dovrebbe mettere un po &#39;di pensiero in quel processo.

Nella mia esperienza, se si pensa al controllo degli accessi e al contenimento, di solito sono buoni driver per la gerarchia dei contenuti. Immaginalo come se fosse il tuo file system. Forse anche utilizzare file e cartelle per modellarlo sul disco locale.

Personalmente preferisco le convenzioni gerarchiche rispetto al sistema di digitazione dei nodi in molti casi inizialmente, e introdurrò la digitazione successivamente.

>[!CAUTION]
>
>Anche il modo in cui è strutturato un archivio di contenuti può influire sulle prestazioni. Per ottenere prestazioni migliori, il numero di nodi figlio associati a singoli nodi in un archivio di contenuti non deve generalmente superare le 1.000.
>
>Vedi [Quanti dati può gestire CRX?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) per ulteriori informazioni.

#### Esempio {#example-2}

Vorrei modellare un semplice sistema di blog come segue. Nota che inizialmente non mi interessa nemmeno i rispettivi nodetype che uso a questo punto.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Credo che una delle cose che emergono sia che tutti comprendiamo la struttura del contenuto basata sull&#39;esempio senza ulteriori spiegazioni.

Ciò che può essere inaspettato inizialmente è il motivo per cui non avrei conservato i &quot;commenti&quot; con il &quot;post&quot;, che è dovuto al controllo dell&#39;accesso che vorrei essere applicato in modo ragionevolmente gerarchico.

Utilizzando il modello di contenuto di cui sopra posso facilmente consentire all&#39;utente &quot;anonimo&quot; di &quot;creare&quot; commenti, ma mantenere l&#39;utente anonimo su una base di sola lettura per il resto dell&#39;area di lavoro.

### Regola n. 3: Le aree di lavoro sono per clone(), merge() e update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Spiegazione {#explanation-3}

Se non utilizzi `clone()`, `merge()` o `update()` metodi nell&#39;applicazione un&#39;unica area di lavoro è probabilmente la strada da seguire.

&quot;nodi corrispondenti&quot; è un concetto definito nelle specifiche JCR. In sostanza, si riduce a nodi che rappresentano lo stesso contenuto, in diverse cosiddette aree di lavoro.

JCR introduce il concetto molto astratto di Workspace che lascia molti sviluppatori incerti su cosa fare con loro. Vorrei proporre di sottoporre a test l&#39;utilizzo degli spazi di lavoro.

Se si dispone di una notevole sovrapposizione di nodi &quot;corrispondenti&quot; (essenzialmente i nodi con lo stesso UUID) in più aree di lavoro, probabilmente le aree di lavoro vengono utilizzate correttamente.

Se non vi è sovrapposizione di nodi con lo stesso UUID, probabilmente si abusano delle aree di lavoro.

Le aree di lavoro non devono essere utilizzate per il controllo degli accessi. La visibilità del contenuto per un particolare gruppo di utenti non è un buon argomento per separare gli elementi in aree di lavoro diverse. JCR dispone di &quot;Controllo accessi&quot; nell’archivio dei contenuti per fornire questo.

Le aree di lavoro sono il limite per riferimenti e query.

#### Esempio {#example-3}

Utilizzare le aree di lavoro per elementi quali:

* v1.2 del progetto rispetto a a v1.3 del progetto
* uno stato di &quot;sviluppo&quot;, &quot;controllo qualità&quot; e di contenuto &quot;pubblicato&quot;

Non utilizzare le aree di lavoro per elementi quali:

* directory home dell&#39;utente
* contenuto distinto per diversi tipi di pubblico target come pubblico, privato, locale, ...
* caselle di posta elettronica per utenti diversi

### Regola n. 4: Attenzione ai fratelli con lo stesso nome. {#rule-beware-of-same-name-siblings}

#### Spiegazione {#explanation-4}

Sebbene SNS (Same Name Siblings) sia stato introdotto nella specifica per consentire la compatibilità con le strutture di dati progettate ed espresse tramite XML e che siano quindi estremamente utili per JCR, SNS presenta un notevole sovraccarico e complessità per l’archivio.

Qualsiasi percorso nell’archivio dei contenuti che contiene un SNS in uno dei suoi segmenti di percorso diventa molto meno stabile. Se un SNS viene rimosso o riordinato, ha un impatto sui percorsi di tutti gli altri SNS e dei relativi figli.

Per l’importazione di XML o l’interazione con SNS XML esistenti può essere necessaria e utile, ma non ho mai utilizzato SNS e mai lo farò nei miei modelli di dati &quot;campo verde&quot;.

#### Esempio {#example-4}

Utilizzare

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

anziché

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Regola n. 5: Riferimenti considerati dannosi. {#rule-references-considered-harmful}

#### Spiegazione {#explanation-5}

I riferimenti implicano l&#39;integrità referenziale. Trovo importante comprendere che i riferimenti non si limitano ad aggiungere costi aggiuntivi per l&#39;archivio che gestisce l&#39;integrità referenziale, ma sono anche costosi dal punto di vista della flessibilità dei contenuti.

Personalmente mi accerto di utilizzare sempre solo i riferimenti quando non sono in grado di gestire un riferimento pericoloso e utilizzare in altro modo un percorso, un nome o una stringa UID per fare riferimento a un altro nodo.

#### Esempio {#example-5}

Supponiamo di consentire &quot;riferimenti&quot; da un documento (a) a un altro documento (b). Se si modella questa relazione utilizzando le proprietà di riferimento, ciò significa che i due documenti sono collegati a livello di archivio. Non è possibile esportare/importare i documenti (a) singolarmente, poiché la destinazione della proprietà di riferimento potrebbe non esistere. Sono interessate anche altre operazioni quali l’unione, l’aggiornamento, il ripristino o il clone.

Quindi, modellerei questi riferimenti come &quot;riferimenti deboli&quot; (in JCR v1.0 questo essenzialmente si riduce alle proprietà della stringa che contengono l&#39;uuid del nodo di destinazione) o semplicemente userei un percorso. A volte il percorso è più significativo per cominciare.

Penso che ci siano casi d&#39;uso in cui un sistema non può davvero funzionare se un riferimento è penzolante, ma non riesco a trovare un buon esempio &quot;reale&quot; ma semplice dalla mia esperienza diretta.

### Regola n. 6: I file sono file. {#rule-files-are-files}

#### Spiegazione {#explanation-6}

Se un modello di contenuto espone qualcosa che anche in remoto *profumo* come un file o una cartella che cerco di utilizzare (o estendere da) `nt:file`, `nt:folder` e `nt:resource`.

Nella mia esperienza molte applicazioni generiche consentono l&#39;interazione con nt:folder e nt:files implicitamente e sanno come gestire e visualizzare tali eventi se sono arricchiti con metadati aggiuntivi. Ad esempio, un&#39;interazione diretta con le implementazioni del file server come CIFS o WebDAV che si trovano sopra JCR diventa implicita.

Penso che come buona regola del pollice si potrebbe usare quanto segue: Se hai bisogno di memorizzare il nome del file e il tipo di MIME allora `nt:file`/ `nt:resource` È un fiammifero molto buono. Se si possono avere più &quot;file&quot; una nt:folder è un buon posto per memorizzarli.

Se devi aggiungere metadati per la risorsa, ad esempio una proprietà &quot;author&quot; o &quot;description&quot;, estendi `nt:resource` non il `nt:file`. Estendo raramente nt:file e frequentemente `nt:resource`.

#### Esempio {#example-6}

Supponiamo che qualcuno voglia caricare un&#39;immagine su un post di blog in:

```xml
/content/myblog/posts/iphone_shipping
```

e forse la reazione istintiva sarebbe aggiungere una proprietà binaria contenente l&#39;immagine.

Anche se ci sono sicuramente buoni casi d&#39;uso per utilizzare solo una proprietà binaria (diciamo che il nome è irrilevante e il mime-type è implicito) in questo caso consiglierei la seguente struttura per il mio esempio di blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regola n. 7: Gli ID sono malvagi. {#rule-ids-are-evil}

#### Spiegazione {#explanation-7}

Nei database relazionali gli ID sono un mezzo necessario per esprimere le relazioni, in modo che le persone tendano ad usarli anche nei modelli di contenuto. Principalmente per le ragioni sbagliate.

Se il modello di contenuto è pieno di proprietà che terminano con &quot;Id&quot;, probabilmente non stai sfruttando correttamente la gerarchia.

È vero che alcuni nodi hanno bisogno di un&#39;identificazione stabile durante il loro ciclo di vita. Molto meno di quello che potreste pensare. mix:referenceable fornisce un tale meccanismo integrato nell&#39;archivio, quindi non c&#39;è davvero bisogno di trovare un ulteriore mezzo per identificare un nodo in modo stabile.

Tieni presente anche che gli elementi possono essere identificati dal percorso, e tanto quanto i &quot;symlink&quot; hanno più senso per la maggior parte degli utenti rispetto ai collegamenti rigidi in un filesystem unix, un percorso ha senso per la maggior parte delle applicazioni fare riferimento a un nodo target.

Ancora più importante, è **mescolare**:referenceable significa che può essere applicata a un nodo nel momento in cui è effettivamente necessario farvi riferimento.

Diciamo quindi che solo perché si desidera essere in grado di fare riferimento potenzialmente a un nodo di tipo &quot;Documento&quot; non significa che il vostro tipo di nodo &quot;Documento&quot; deve estendersi da mix:referenceable in modo statico in quanto può essere aggiunto a qualsiasi istanza del &quot;Documento&quot; dinamicamente.

#### Esempio {#example-7}

Utilizzare:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

anziché:

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```
