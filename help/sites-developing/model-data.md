---
title: Modellazione dati - Modello di David Nuescheler
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

# Modellazione dati - Modello di David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Sorgente {#source}

Di seguito sono riportate le idee e i commenti espressi da David Nuescheler.

David è stato co-fondatore e CTO di Day Software AG, uno dei principali fornitori di software per la gestione dei contenuti e l&#39;infrastruttura dei contenuti globali, acquisito da Adobe nel 2010. È stato membro e vicepresidente della divisione Enterprise Technology di Adobe e guida lo sviluppo di JSR-170, l&#39;API Java Content Repository (JCR), lo standard tecnologico per la gestione dei contenuti.

Ulteriori aggiornamenti sono disponibili su [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## Introduzione di David {#introduction-from-david}

In varie discussioni ho riscontrato che gli sviluppatori sono in qualche modo a disagio con le funzioni e le funzionalità presentate da JCR quando si tratta di modellazione dei contenuti. Non esiste ancora una guida e un’esperienza molto limitata su come modellare il contenuto in un archivio e sul perché un modello di contenuto è migliore dell’altro.

Anche se nel mondo relazionale il settore del software ha molta esperienza su come modellare i dati, siamo ancora alle fasi iniziali per lo spazio dell&#39;archivio dei contenuti.

Vorrei iniziare a riempire questo vuoto esprimendo le mie opinioni personali su come il contenuto dovrebbe essere modellato, sperando che questo potrebbe un giorno laurearsi in qualcosa di più significativo per la comunità degli sviluppatori, che non è solo &quot;la mia opinione&quot;, ma qualcosa di più genericamente applicabile. Considerate questo come la mia prima pugnalata che si evolve rapidamente.

>[!NOTE]
>
>Dichiarazione di non responsabilità: queste linee guida esprimono le mie opinioni personali, a volte controverse. Sono ansioso di discutere questi orientamenti e di perfezionarli.

## Sette regole semplici {#seven-simple-rules}

### Regola #1: dati prima, struttura dopo. Forse. {#rule-data-first-structure-later-maybe}

#### Spiegazione {#explanation-1}

Raccomando di non preoccuparsi di una struttura di dati dichiarata in senso ERD. Inizialmente.

Scopri come amare nt:unstructured (&amp; friends) nello sviluppo.

Penso che Stefano riesca a riassumere più o meno questo.

Il mio punto di vista: la struttura è costosa e in molti casi non è assolutamente necessario dichiarare esplicitamente la struttura nello storage sottostante.

Esiste un contratto implicito relativo alla struttura utilizzata intrinsecamente dall&#39;applicazione. Supponiamo che memorizzi la data di modifica di un post di blog in una proprietà lastModified. La mia app saprà automaticamente di leggere di nuovo la data di modifica dalla stessa proprietà, non c’è davvero bisogno di dichiararla esplicitamente.

Ulteriori vincoli sui dati, come i vincoli obbligatori o di tipo e valore, devono essere applicati solo se necessario per motivi di integrità dei dati.

#### Esempio {#example-1}

L’esempio precedente di utilizzo di una `lastModified` La proprietà della data, ad esempio sul nodo &quot;post di blog&quot;, non significa necessariamente che sia necessario un tipo di nodo speciale. Userei sicuramente `nt:unstructured` almeno inizialmente per i nodi del post di blog. Dato che nella mia applicazione di blogging tutto quello che sto per fare è quello di visualizzare la data ultima modificata comunque (possibilmente &quot;ordina per&quot;) mi importa a malapena se è una data affatto. Dato che implicitamente mi fido della mia applicazione di scrittura di blog per mettere un &quot;data&quot; lì comunque, non c&#39;è davvero bisogno di dichiarare la presenza di un `lastModified` data nella forma a di nodetype.

### Regola #2: guida la gerarchia dei contenuti, non lasciare che accada. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Spiegazione {#explanation-2}

La gerarchia dei contenuti è una risorsa molto preziosa. Quindi non lasciate che accada, progettatelo. Se non hai un nome &quot;buono&quot; e leggibile per un nodo, è probabilmente qualcosa che dovresti riconsiderare. I numeri arbitrari non sono quasi mai un &quot;buon nome&quot;.

Anche se può essere estremamente facile mettere rapidamente un modello relazionale esistente in un modello gerarchico, si dovrebbe mettere un po &#39;di pensiero in quel processo.

Nella mia esperienza, se si pensa al controllo degli accessi e al contenimento, in genere si tratta di fattori validi per la gerarchia dei contenuti. Immaginatelo come se fosse il vostro file system. È possibile utilizzare anche file e cartelle per modellarli sul disco locale.

Personalmente preferisco le convenzioni gerarchiche rispetto al sistema di nodetyping in molti casi inizialmente, e introduco la digitazione in un secondo momento.

>[!CAUTION]
>
>La struttura di un archivio di contenuti può influire anche sulle prestazioni. Per prestazioni ottimali, il numero di nodi secondari collegati ai singoli nodi in un archivio di contenuti non deve in genere superare le 1.000 unità.
>
>Consulta [Quanti dati può gestire CRX?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) per ulteriori informazioni.

#### Esempio {#example-2}

Modellerei un semplice sistema di blog come segue. Tieni presente che inizialmente non mi interessano nemmeno i rispettivi tipi di noduli che utilizzo a questo punto.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Credo che una delle cose che diventano evidenti è che tutti comprendiamo la struttura del contenuto basata sull&#39;esempio senza ulteriori spiegazioni.

Ciò che inizialmente può essere inaspettato è il motivo per cui non memorizzerei i &quot;commenti&quot; con il &quot;post&quot;, che è dovuto al controllo degli accessi che vorrei essere applicato in modo ragionevolmente gerarchico.

Utilizzando il modello di contenuto di cui sopra posso consentire facilmente all’utente &quot;anonimo&quot; di &quot;creare&quot; commenti, ma mantenere l’utente anonimo in sola lettura per il resto dell’area di lavoro.

### Regola #3: le aree di lavoro sono per clone(), merge() e update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Spiegazione {#explanation-3}

Se non usi `clone()`, `merge()` o `update()` metodi nell&#39;applicazione un&#39;unica area di lavoro è probabilmente la soluzione ideale.

&quot;Nodi corrispondenti&quot; è un concetto definito nelle specifiche JCR. In sostanza, si riduce ai nodi che rappresentano lo stesso contenuto, in diverse cosiddette aree di lavoro.

JCR introduce il concetto molto astratto di aree di lavoro che lascia molti sviluppatori non chiari su cosa fare con loro. Vorrei proporre di testare l’utilizzo delle aree di lavoro da parte tua.

Se si dispone di una notevole sovrapposizione di nodi &quot;corrispondenti&quot; (essenzialmente i nodi con lo stesso UUID) in più aree di lavoro, è probabile che le aree di lavoro vengano utilizzate correttamente.

Se non vi è alcuna sovrapposizione di nodi con lo stesso UUID, probabilmente stai abusando delle aree di lavoro.

Le aree di lavoro non devono essere utilizzate per il controllo degli accessi. La visibilità dei contenuti per un particolare gruppo di utenti non è un buon argomento per separare gli elementi in aree di lavoro diverse. JCR dispone del &quot;Controllo degli accessi&quot; nell’archivio dei contenuti.

Le aree di lavoro sono il limite per i riferimenti e le query.

#### Esempio {#example-3}

Utilizza le aree di lavoro per:

* v1.2 del progetto rispetto alla v1.3 del progetto
* uno stato di &quot;sviluppo&quot;, &quot;QA&quot; e uno stato di &quot;pubblicazione&quot; del contenuto

Non utilizzare le aree di lavoro per elementi quali:

* home directory utente
* contenuti distinti per tipi di pubblico diversi, come pubblico, privato, locale, ...
* caselle di posta per utenti diversi

### Regola #4: attenzione ai pari livello con lo stesso nome. {#rule-beware-of-same-name-siblings}

#### Spiegazione {#explanation-4}

Sebbene nella specifica siano stati introdotti elementi di pari livello con lo stesso nome (SNS, Same Name Siblings) per consentire la compatibilità con strutture di dati progettate ed espresse tramite XML e pertanto estremamente utili per JCR, SNS presenta un sovraccarico e una complessità considerevoli per l’archivio.

Qualsiasi percorso all’interno dell’archivio dei contenuti che contiene un SNS in uno dei suoi segmenti di percorso diventa molto meno stabile; se un SNS viene rimosso o riordinato, ha un impatto sui percorsi di tutti gli altri SNS e dei relativi elementi secondari.

Per l&#39;importazione di XML o l&#39;interazione con gli SNS XML esistenti può essere necessario e utile, ma non ho mai utilizzato SNS e non lo farò mai nei miei modelli di dati &quot;green field&quot;.

#### Esempio {#example-4}

Utilizzare

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

invece di

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Regola #5: riferimenti considerati dannosi. {#rule-references-considered-harmful}

#### Spiegazione {#explanation-5}

I riferimenti implicano integrità referenziale. È importante comprendere che i riferimenti non solo aggiungono costi aggiuntivi per l’archivio gestendo l’integrità referenziale, ma sono anche costosi dal punto di vista della flessibilità dei contenuti.

Personalmente, mi assicuro di utilizzare sempre i riferimenti solo quando non riesco davvero a gestire un riferimento penzolante e altrimenti utilizzo un percorso, un nome o una stringa UUID per fare riferimento a un altro nodo.

#### Esempio {#example-5}

Supponiamo che io permetta &quot;riferimenti&quot; da un documento (a) a un altro documento (b). Se si modella questa relazione utilizzando le proprietà di riferimento, significa che i due documenti sono collegati a livello di repository. Non è possibile esportare/importare singolarmente il documento (a), poiché la destinazione della proprietà di riferimento potrebbe non esistere. Sono interessate anche altre operazioni quali unione, aggiornamento, ripristino o clonazione.

Quindi modellerei quei riferimenti come &quot;riferimenti deboli&quot; (in JCR v1.0 questo si riduce essenzialmente alle proprietà stringa che contengono l’UUID del nodo di destinazione) o semplicemente utilizzerei un percorso. A volte il percorso è più significativo per iniziare.

Penso che ci siano casi d&#39;uso in cui un sistema non può davvero funzionare se un riferimento è penzolante, ma semplicemente non riesco a trovare un buon esempio &quot;reale&quot; ma semplice dalla mia esperienza diretta.

### Regola #6: i file sono file. {#rule-files-are-files}

#### Spiegazione {#explanation-6}

Se un modello di contenuto espone qualcosa che anche in remoto *odori* come un file o una cartella che tento di utilizzare (o estendere da) `nt:file`, `nt:folder` e `nt:resource`.

Nella mia esperienza, molte applicazioni generiche consentono l’interazione con nt:folder e nt:files in modo implicito e sanno come gestire e visualizzare tali eventi se arricchiti da metadati aggiuntivi. Ad esempio, un’interazione diretta con implementazioni di file server come CIFS o WebDAV che si trovano sopra JCR diventa implicita.

Penso che come buona regola generale si potrebbe usare quanto segue: Se avete bisogno di memorizzare il nome del file e il tipo di mime allora `nt:file`/ `nt:resource` è un&#39;ottima combinazione. Se si possono avere più &quot;file&quot;, la cartella nt:folder è un buon punto in cui memorizzarli.

Se devi aggiungere metadati per la risorsa, ad esempio una proprietà &quot;author&quot; o &quot;description&quot;, estendi `nt:resource` non il `nt:file`. Estendo raramente nt:file ed estendo frequentemente `nt:resource`.

#### Esempio {#example-6}

Supponiamo che qualcuno voglia caricare un&#39;immagine in un post di blog all&#39;indirizzo:

```xml
/content/myblog/posts/iphone_shipping
```

e forse la reazione istintiva iniziale sarebbe di aggiungere una proprietà binaria contenente l&#39;immagine.

Anche se ci sono sicuramente casi d’uso validi per utilizzare solo una proprietà binaria (supponiamo che il nome sia irrilevante e il tipo mime implicito) in questo caso consiglierei la seguente struttura per il mio esempio di blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regola #7: gli ID sono malvagi. {#rule-ids-are-evil}

#### Spiegazione {#explanation-7}

Nei database relazionali gli ID sono un mezzo necessario per esprimere le relazioni, quindi le persone tendono a utilizzarli anche nei modelli di contenuto. Soprattutto per i motivi sbagliati.

Se il modello di contenuto è pieno di proprietà che terminano con &quot;Id&quot;, è probabile che la gerarchia non venga sfruttata correttamente.

È vero che alcuni nodi necessitano di un’identificazione stabile durante il loro ciclo di vita. Molto meno di quanto possiate immaginare. mix:referenceable fornisce un meccanismo di questo tipo integrato nell&#39;archivio, pertanto non è necessario trovare un metodo aggiuntivo per identificare un nodo in modo stabile.

Tieni presente che gli elementi possono essere identificati in base al percorso e che i &quot;symlink&quot; hanno più senso per la maggior parte degli utenti rispetto ai collegamenti rigidi in un file system unix, un percorso ha un senso per la maggior parte delle applicazioni fare riferimento a un nodo di destinazione.

Ma, soprattutto, **mix**:referenceable significa che può essere applicato a un nodo nel momento in cui è effettivamente necessario farvi riferimento.

Supponiamo quindi che solo perché si desidera essere potenzialmente in grado di fare riferimento a un nodo di tipo &quot;Documento&quot; non significa che il tipo di nodo &quot;Documento&quot; debba estendersi da mix:referenziabile in modo statico, in quanto può essere aggiunto dinamicamente a qualsiasi istanza del &quot;Documento&quot;.

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
