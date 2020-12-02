---
title: Modellazione dei dati - Modello di David Nuescheler
seo-title: Modellazione dei dati - Modello di David Nuescheler
description: Raccomandazioni di David Nuescheler sulla modellazione dei contenuti
seo-description: Raccomandazioni di David Nuescheler sulla modellazione dei contenuti
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---


# Modellazione dei dati - Modello di David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Origine {#source}

I seguenti dettagli sono idee e commenti espressi da David Nuescheler.

David è stato co-fondatore e CTO of Day Software AG, uno dei principali fornitori di software globali per la gestione dei contenuti e l&#39;infrastruttura dei contenuti, richiesto  Adobe nel 2010. È ora membro e vicepresidente di Enterprise Technology  Adobe e guida lo sviluppo di JSR-170, l&#39;API (Application Programming Interface) Java Content Repository (JCR), lo standard tecnologico per la gestione dei contenuti.

Ulteriori aggiornamenti sono disponibili anche su [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## Introduzione da David {#introduction-from-david}

In varie discussioni ho scoperto che gli sviluppatori sono in qualche modo a disagio con le caratteristiche e funzionalità presentate da JCR quando si tratta di modellazione del contenuto. Non esiste una guida e non c&#39;è ancora molta esperienza su come modellare il contenuto in un repository e sul motivo per cui un modello di contenuto è migliore dell&#39;altro.

Mentre nel mondo relazionale l&#39;industria del software ha molta esperienza su come modellare i dati, siamo ancora alle prime fasi per lo spazio archivio dei contenuti.

Vorrei iniziare a riempire questo vuoto esprimendo le mie opinioni personali su come il contenuto dovrebbe essere modellato, sperando che un giorno possa diventare qualcosa di più significativo per la comunità degli sviluppatori, che non è solo &quot;la mia opinione&quot;, ma qualcosa di più generale applicabile. Considerate questo mio primo attacco in rapida evoluzione.

>[!NOTE]
>
>Dichiarazione di non responsabilità: Queste linee guida esprimono le mie opinioni personali, talvolta controverse. Sono ansioso di discutere di questi orientamenti e di perfezionarli.

## Sette regole semplici {#seven-simple-rules}

### Regola n. 1: Prima i dati, poi la struttura. Forse. {#rule-data-first-structure-later-maybe}

#### Spiegazione {#explanation-1}

Raccomando di non preoccuparsi di una struttura di dati dichiarata in senso ERD. Inizialmente.

Imparare ad amare non:non strutturati (&amp;) nello sviluppo.

Credo che Stefano riassuma questo.

La mia linea di fondo: La struttura è costosa e in molti casi non è assolutamente necessario dichiarare esplicitamente la struttura allo stoccaggio sottostante.

Esiste un contratto implicito sulla struttura che l&#39;applicazione utilizza in modo intrinseco. Supponiamo di memorizzare la data di modifica di un post di blog in una proprietà lastModified. La mia App saprà automaticamente leggere la data di modifica di quella stessa proprietà, non c&#39;è davvero bisogno di dichiararlo esplicitamente.

Ulteriori vincoli relativi ai dati, come i vincoli obbligatori o di tipo e di valore, dovrebbero essere applicati solo se necessario per motivi di integrità dei dati.

#### Esempio {#example-1}

L&#39;esempio precedente relativo all&#39;utilizzo di una proprietà `lastModified` Date, ad esempio il nodo &quot;post blog&quot;, non significa in realtà che sia necessario un tipo di nodo speciale. Utilizzerei sicuramente `nt:unstructured` per i nodi post del mio blog almeno inizialmente. Dal momento che nella mia applicazione di blog tutto ciò che farò è mostrare la data dell&#39;ultima modifica comunque (forse &quot;ordine entro&quot;) mi importa a malapena se è un Data. Dato che mi fido implicitamente della mia applicazione di scrittura di blog per inserire una &quot;data&quot; comunque, non c&#39;è davvero bisogno di dichiarare la presenza di una data `lastModified` nella forma di un nodetype.

### Regola n. 2: Guidare la gerarchia dei contenuti, non lasciarla accadere. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Spiegazione {#explanation-2}

La gerarchia dei contenuti è una risorsa molto preziosa. Quindi non lasciate che accada, progettatelo. Se non avete un nome &quot;buono&quot; e leggibile per un nodo, probabilmente è qualcosa che dovreste riconsiderare. I numeri arbitrari non sono mai un &quot;buon nome&quot;.

Anche se può essere estremamente facile mettere rapidamente un modello relazionale esistente in un modello gerarchico, si dovrebbe riflettere in quel processo.

Nella mia esperienza, se si pensa al controllo degli accessi e al contenimento, in genere buoni driver per la gerarchia dei contenuti. Pensatelo come se fosse il vostro file system. Forse anche utilizzare file e cartelle per modellare sul disco locale.

Personalmente preferisco le convenzioni gerarchiche rispetto al sistema di digitazione dei nodi in molti casi inizialmente, e introdurre la digitazione successivamente.

>[!CAUTION]
>
>Anche la struttura di un archivio dei contenuti può avere un impatto sulle prestazioni. Per ottenere prestazioni ottimali, il numero di nodi secondari associati a singoli nodi in un archivio dei contenuti non deve in genere superare 1000.
>
>Vedere [Quanti dati è in grado di gestire CRX?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) per ulteriori informazioni.

#### Esempio {#example-2}

Vorrei modellare un semplice sistema di blog come segue. Nota che inizialmente non mi interessa nemmeno i rispettivi tipi di nodi che uso a questo punto.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Credo che una delle cose che si sono rese evidenti è che tutti comprendiamo la struttura del contenuto basata sull&#39;esempio senza ulteriori spiegazioni.

Ciò che potrebbe essere inaspettato inizialmente è il motivo per cui non avrei memorizzato i &quot;commenti&quot; con il &quot;post&quot;, che è dovuto al controllo di accesso che mi piacerebbe essere applicato in modo ragionevolmente gerarchico.

Utilizzando il modello di contenuto sopra riportato, posso facilmente consentire all&#39;utente &quot;anonimo&quot; di &quot;creare&quot; commenti, ma mantenere l&#39;utente anonimo in sola lettura per il resto dell&#39;area di lavoro.

### Regola n. 3: Le aree di lavoro sono per clone(), merge() e update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Spiegazione {#explanation-3}

Se non si utilizzano i metodi `clone()`, `merge()` o `update()` nell&#39;applicazione, è probabile che un&#39;unica area di lavoro sia la strada da seguire.

&quot;nodi corrispondenti&quot; è un concetto definito nella specifica JCR. Essenzialmente, si riduce a nodi che rappresentano lo stesso contenuto, in diverse aree di lavoro.

JCR introduce il concetto molto astratto di Workspaces che lascia molti sviluppatori poco chiari su cosa fare con loro. Vorrei proporre di sottoporre a test l&#39;uso dei vostri spazi di lavoro.

Se si ha una sovrapposizione notevole di nodi &quot;corrispondenti&quot; (essenzialmente i nodi con lo stesso UUID) in più aree di lavoro, è probabile che le aree di lavoro siano utili.

Se non vi è sovrapposizione di nodi con lo stesso UUID, probabilmente si abuseranno di aree di lavoro.

Le aree di lavoro non devono essere utilizzate per il controllo degli accessi. La visibilità del contenuto per un particolare gruppo di utenti non è un buon argomento per separare gli elementi in aree di lavoro diverse. JCR dispone di &quot;Controllo accesso&quot; nell&#39;archivio dei contenuti per fornire tali informazioni.

Le aree di lavoro sono il limite per riferimenti e query.

#### Esempio {#example-3}

Utilizzare aree di lavoro per attività quali:

* v1.2 del progetto rispetto a v1.3 del progetto
* uno stato di &quot;sviluppo&quot;, &quot;QA&quot; e &quot;pubblicato&quot;

Non utilizzate aree di lavoro per elementi quali:

* directory home utente
* contenuto distinto per diversi tipi di pubblico target come pubblico, privato, locale, ...
* caselle di posta elettronica per diversi utenti

### Regola n. 4: Fai attenzione ai fratelli con lo stesso nome. {#rule-beware-of-same-name-siblings}

#### Spiegazione {#explanation-4}

Mentre SNS (Same Name Siblings) è stato introdotto nella specifica per consentire la compatibilità con le strutture di dati progettate per e espresse tramite XML e quindi estremamente preziose per JCR, SNS presenta un sovraccarico e una complessità notevoli per il repository.

Qualsiasi percorso all&#39;interno dell&#39;archivio dei contenuti che contiene un SNS in uno dei suoi segmenti di percorso diventa molto meno stabile. Se un SNS viene rimosso o riordinato, questo avrà un impatto sui percorsi di tutti gli altri SNS e dei relativi elementi secondari.

Per l&#39;importazione di XML o per l&#39;interazione con SNS XML esistenti può essere necessario e utile, ma non ho mai utilizzato SNS e non lo sarà mai nei miei modelli di dati &quot;campo verde&quot;.

#### Esempio {#example-4}

Utilizzo

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

I riferimenti implicano l&#39;integrità referenziale. È importante comprendere che i riferimenti non comportano solo un costo aggiuntivo per il repository che gestisce l&#39;integrità referenziale, ma sono anche costosi dal punto di vista della flessibilità dei contenuti.

Personalmente mi assicuro di utilizzare sempre i riferimenti solo quando non riesco davvero a gestire un riferimento pericoloso e altrimenti uso un percorso, un nome o una stringa UUID per fare riferimento a un altro nodo.

#### Esempio {#example-5}

Supponiamo di consentire &quot;riferimenti&quot; da un documento (a) a un altro documento (b). Se faccio un modello di questa relazione utilizzando le proprietà di riferimento, ciò significa che i due documenti sono collegati a livello di repository. Non è possibile esportare/importare documenti (a) singolarmente, poiché la destinazione della proprietà di riferimento potrebbe non esistere. Vengono interessate anche altre operazioni quali unione, aggiornamento, ripristino o duplicazione.

Quindi potrei modellare questi riferimenti come &quot;riferimenti deboli&quot; (in JCR v1.0 questo sostanzialmente si riduce a proprietà stringa che contengono l&#39;uuid del nodo di destinazione) o semplicemente utilizzare un percorso. A volte il percorso è più significativo da iniziare.

Penso che ci siano casi d&#39;uso in cui un sistema non può realmente funzionare se un riferimento è penzolante, ma non riesco a trovare un buon esempio &quot;reale&quot; ma semplice dalla mia esperienza diretta.

### Regola n. 6: I file sono file. {#rule-files-are-files}

#### Spiegazione {#explanation-6}

Se un modello di contenuto espone qualcosa che ha un odore anche remoto *come un file o una cartella che cerco di utilizzare (o estendere da) `nt:file`, `nt:folder` e `nt:resource`.*

Nella mia esperienza molte applicazioni generiche consentono l&#39;interazione con nt:folder e nt:files in modo implicito e sanno come gestire e visualizzare tali eventi se sono arricchiti con ulteriori metadati. Ad esempio, un&#39;interazione diretta con le implementazioni del file server come CIFS o WebDAV che si trovano sopra JCR diventa implicita.

Credo che, come buona regola del pollice, si possa usare quanto segue: Se è necessario memorizzare il nome del file e il tipo mime, `nt:file`/ `nt:resource` è una corrispondenza molto buona. Se si possono avere più &quot;file&quot;, un nt:folder è un buon punto in cui memorizzarli.

Se è necessario aggiungere metadati alla risorsa, ad esempio una proprietà &quot;author&quot; o &quot;description&quot;, estendere `nt:resource` non la `nt:file`. Estendo raramente nt:file e estendendo frequentemente `nt:resource`.

#### Esempio {#example-6}

Supponiamo che qualcuno voglia caricare un&#39;immagine in un post del blog all&#39;indirizzo:

```xml
/content/myblog/posts/iphone_shipping
```

e forse la reazione iniziale dell&#39;intestino sarebbe di aggiungere una proprietà binaria che contiene l&#39;immagine.

Anche se ci sono sicuramente buoni casi d&#39;uso per utilizzare solo una proprietà binaria (diciamo che il nome è irrilevante e il mime-type è implicito) in questo caso, consiglierei la seguente struttura per il mio esempio di blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regola n. 7: Gli ID sono malvagi. {#rule-ids-are-evil}

#### Spiegazione {#explanation-7}

Nei database relazionali gli ID sono un mezzo necessario per esprimere le relazioni, in modo che le persone tendono ad utilizzarli anche nei modelli di contenuto. Principalmente per le ragioni sbagliate.

Se il modello di contenuto è pieno di proprietà che terminano con &quot;Id&quot;, probabilmente non state sfruttando correttamente la gerarchia.

È vero che alcuni nodi necessitano di un&#39;identificazione stabile durante tutto il loro ciclo di vita. Molto meno di quanto potresti pensare. mix:referenceable fornisce un meccanismo di questo tipo integrato nel repository, quindi non c&#39;è davvero bisogno di trovare un modo aggiuntivo per identificare un nodo in modo stabile.

Tenete anche presente che gli elementi possono essere identificati per percorso, e tanto più che &quot;symlinks&quot; ha senso per la maggior parte degli utenti che non i collegamenti diretti in un file system unix, un percorso ha senso per la maggior parte delle applicazioni fare riferimento a un nodo di destinazione.

Inoltre, è **mix**:referenceable, il che significa che può essere applicato a un nodo nel momento in cui è effettivamente necessario farvi riferimento.

Diciamo che solo perché si desidera poter fare riferimento potenzialmente a un nodo di tipo &quot;Documento&quot; non significa che il tipo di nodo &quot;Documento&quot; deve estendersi da mix:referenceable in modo statico, in quanto può essere aggiunto a qualsiasi istanza del &quot;Documento&quot; in modo dinamico.

#### Esempio {#example-7}

Utilizzo:

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

