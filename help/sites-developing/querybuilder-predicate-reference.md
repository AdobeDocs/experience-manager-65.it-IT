---
title: Riferimento predicato Query Builder
seo-title: Riferimento predicato Query Builder
description: Riferimento predicato completo per l'API Query Builder.
seo-description: Riferimento predicato completo per l'API Query Builder.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Riferimento predicato Query Builder{#query-builder-predicate-reference}

## Generale {#general}

* [root](#root)
* [gruppo](#group)
* [ordine](#orderby)

## Predicati {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentFragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [fulltext](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [language](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [principale](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [MemberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [not](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [path](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [proprietà](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [similar](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [tipo](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Corrisponde alle proprietà JCR BOOLEAN. Accetta solo i valori &quot; `true`&quot; e &quot; `false`&quot;. In caso di &quot; `false`&quot;, corrisponderà se la proprietà ha il valore &quot; `false`&quot; o se non esiste affatto. Questa funzione può essere utile per verificare la presenza di flag booleani impostati solo se abilitati.

Il parametro &quot; `operation`&quot; ereditato non ha alcun significato.

Supporta l&#39;estrazione dei facet. Fornirà bucket per ogni `true` o `false` valore, ma solo per le proprietà esistenti.

#### Proprietà {#properties}

* **boolproperty** percorso relativo alla proprietà, ad esempio `myFeatureEnabled` o `jcr:content/myFeatureEnabled`

* **value** value to check property for, &quot; `true`&quot; or &quot; `false`&quot;

### contentfragment {#contentfragment}

Limita il risultato ai frammenti di contenuto.

Non supporta il filtro.

Non supporta l&#39;estrazione facet.

#### Proprietà {#properties-1}

* **frammento di contenuto** Può essere utilizzato con qualsiasi valore per verificare la presenza di frammenti di contenuto.

### dateComparison {#datecomparison}

Confronta tra loro due proprietà JCR DATE. Può verificare se sono uguali, diversi, maggiori o maggiori di o uguali.

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca.

#### Proprietà {#properties-2}

* **property1**

   percorso della prima proprietà data

* **property2**

   percorso della proprietà seconda data

* **operation**

   &quot; `=`&quot; per corrispondenza esatta, &quot; `!=`&quot; per confronto di non uguaglianza, &quot; `>`&quot; per proprietà1 maggiore di property2, &quot; `>=`&quot; per proprietà1 maggiore o uguale a property2. Il valore predefinito è &quot; `=`&quot;.

### daterange {#daterange}

Corrisponde alle proprietà DATA JCR rispetto a un intervallo data/ora. Questo utilizza il formato ISO8601per date e ore ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) e consente anche rappresentazioni parziali, come `YYYY-MM-DD`. In alternativa, la marca temporale può essere fornita come numero di millisecondi a partire dal 1970 nel fuso orario UTC, il formato ora uniforme.

Potete cercare qualsiasi elemento tra due marche temporali, qualsiasi data più recente o precedente, e scegliere anche tra intervalli inclusivi e aperti.

Supporta l&#39;estrazione dei facet. Fornirà i secchi &quot;oggi&quot;, &quot;questa settimana&quot;, &quot;questo mese&quot;, &quot;ultimi 3 mesi&quot;, &quot;quest&#39;anno&quot;, &quot;l&#39;anno scorso&quot; e &quot;prima dello scorso anno&quot;.

Non supporta il filtro.

#### Proprietà {#properties-3}

* **proprietà**

   percorso relativo a una `DATE` proprietà, ad esempio `jcr:lastModified`

* **lowerBound**

   data inferiore associata a check property, ad esempio `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (più recente) o &quot; `>=`&quot; (più recente o più recente), si applica al `lowerBound`. Il valore predefinito è &quot; `>`&quot;.

* **UpperBound**

   Upper bound to check property, ad esempio `2014-10-01T12:15:00`

* **UpperOperation**

   &quot; `<`&quot; (precedente) o &quot; `<=`&quot; (precedente o precedente), si applica al `upperBound`. Il valore predefinito è &quot; `<`&quot;.

* **timeZone**

   ID del fuso orario da utilizzare quando non viene specificato come stringa data ISO-8601. L&#39;impostazione predefinita è il fuso orario predefinito del sistema.

### excludepaths {#excludepaths}

Esclude i nodi dal risultato se il percorso corrisponde a un&#39;espressione regolare.

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca.

Non supporta l&#39;estrazione facet.

#### Proprietà {#properties-4}

* **excludepaths**

   espressione regolare confrontata con i percorsi dei risultati, escludendo quelli corrispondenti dal risultato.

### fulltext {#fulltext}

Cerca i termini nell&#39;indice full-text.

Non supporta il filtro.

Non supporta l&#39;estrazione facet.

#### Proprietà {#properties-5}

* **fulltext**

   termini di ricerca full-text

* **relPath**

   percorso relativo da cercare nella proprietà o nel nodo secondario. Questa proprietà è facoltativa.

### gruppo {#group}

Consente di creare condizioni nidificate. I gruppi possono contenere gruppi nidificati. Tutto in una query querybuilder è implicitamente in un gruppo principale, che può avere `p.or` e `p.not` anche parametri.

Esempio di corrispondenza tra una delle due proprietà e un valore:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Questo è concettualmente `(1_property` O `2_property)`.

Esempio per i gruppi nidificati:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Viene ricercato il termine &quot;**Gestione**&quot; all’interno delle pagine `/content/geometrixx/en` o nelle risorse in `/content/dam/geometrixx`.

Questo è concettualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Tenere presente che tali join OR richiedono buoni indici per le prestazioni.

#### Proprietà {#properties-6}

* **p.or**

   se è impostato su &quot; `true`&quot;, solo un predicato nel gruppo deve corrispondere. Questo valore predefinito è &quot; `false`&quot;, ovvero tutti devono corrispondere

* **p.not**

   se impostato su &quot; `true`&quot;, nega il gruppo (per impostazione predefinita, su &quot; `false`&quot;)

* **&lt;predicate>**

   aggiunge predicati nidificati

* **N_&lt;predicato>**

   aggiunge più predicati nidificati contemporaneamente, come `1_property, 2_property, ...`

### hasPermission {#haspermission}

Limita il risultato agli elementi in cui la sessione corrente dispone dei privilegi [JCR specificati.](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca. Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-7}

* **hasPermission**

   privilegi JCR separati da virgola che la sessione utente corrente deve avere per il nodo in questione; ad esempio `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Trova le pagine CQ in una lingua specifica. Questo esamina sia la proprietà della lingua della pagina che il percorso della pagina, che spesso include la lingua o le impostazioni internazionali in una struttura del sito di livello principale.

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca.

Supporta l&#39;estrazione dei facet. Forniranno bucket per ogni codice di lingua univoco.

#### Proprietà {#properties-8}

* **language**

   Codice della lingua ISO, ad esempio &quot; `de`&quot;

### principale {#mainasset}

Controlla se un nodo è una risorsa principale DAM e non una risorsa secondaria. In pratica, si tratta di ogni nodo non incluso in un nodo &quot;subassets&quot;. Si noti che questo non verifica il tipo di `dam:Asset` nodo. Per utilizzare questo predicato, impostare semplicemente &quot; `mainasset=true`&quot; o &quot; `mainasset=false`&quot;, non ci sono ulteriori proprietà.

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca.

Supporta l&#39;estrazione dei facet. Fornirà 2 socket per risorse principali e secondarie.

#### Proprietà {#properties-9}

* **principale**

   booleano, &quot; `true`&quot; per le risorse principali, &quot; `false`&quot; per le risorse secondarie

### MemberOf {#memberof}

Trova gli elementi che fanno parte di una raccolta [di risorse](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)sling specifica.

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca. Non supporta l&#39;estrazione facet.

#### Proprietà {#properties-10}

* **MemberOf**

   percorso della raccolta di risorse Sling

### nodename {#nodename}

Corrisponde ai nomi dei nodi JCR.

Supporta l&#39;estrazione dei facet. Fornirà bucket per ogni nome di nodo univoco (nome file).

#### Proprietà {#properties-11}

* **nodename**

   pattern di nome nodo che consente i caratteri jolly: `*` = qualsiasi o nessun carattere, `?` = qualsiasi carattere, `[abc]` = solo caratteri tra parentesi

### not {#notexpired}

Corrisponde agli elementi controllando se una proprietà JCR DATE è maggiore o uguale all&#39;ora del server corrente. Può essere utilizzato per controllare una proprietà &quot; `expiresAt`&quot; come date e limitare solo a quelle che non sono ancora scadute ( `notexpired=true`) o che sono già scadute ( `notexpired=false`).

Non supporta il filtro.

Supporta l&#39;estrazione dei facet nello stesso modo del predicato daterange.

#### Proprietà {#properties-12}

* **not**

   booleano, &quot; `true`&quot; per non ancora scaduto (data in futuro o uguale), &quot; `false`&quot; per scaduto (data in passato) (obbligatorio)

* **proprietà**

   percorso relativo alla `DATE` proprietà da verificare (obbligatorio)

### ordine {#orderby}

Consente di ordinare il risultato. Se l&#39;ordine è richiesto da più proprietà, questo predicato deve essere aggiunto più volte utilizzando il prefisso numerico, ad esempio `1_orderby=first`, `2_oderby=second`.

#### Proprietà {#properties-13}

* **ordine**

   il nome della proprietà JCR indicato da una @ iniziale, ad esempio `@jcr:lastModified` o `@jcr:content/jcr:title`, oppure da un altro predicato nella query, ad esempio `2_property`, sul quale eseguire l&#39;ordinamento.

* **ordina**

   direzione di ordinamento, &quot; `desc`&quot; per discendente o &quot; `asc`&quot; per crescente (predefinita)

* **case**

   se impostato su &quot; `ignore`&quot; renderà insensibile la distinzione tra maiuscole e minuscole, il che significa che &quot;a&quot; precede &quot;B&quot;; se vuoto o omesso, l&#39;ordinamento è sensibile alle maiuscole/minuscole, il che significa &quot;B&quot; precede &quot;a&quot;

### path {#path}

Ricerche all’interno di un determinato percorso.

Non supporta l&#39;estrazione facet.

#### Proprietà {#properties-14}

* **path**

   modello di percorso; in base all&#39;esatta, l&#39;intera sottostruttura corrisponderà (come l&#39;aggiunta `//*` in xpath, ma si noti che non include il percorso di base) (exact=false, default) o solo una corrispondenza esatta del percorso, che può includere caratteri jolly ( `*`); se è impostato su se stesso, verrà eseguita la ricerca nell&#39;intera sottostruttura, incluso il nodo di base

* **exact**

   se `exact` è true/on, il percorso esatto deve corrispondere, ma può contenere caratteri jolly semplici ( `*`), che corrispondono ai nomi, ma non &quot; `/`&quot;; se è false (impostazione predefinita), tutti i discendenti sono inclusi (facoltativo)

* **piatto**

   esegue la ricerca solo negli elementi figlio diretti (come l&#39;aggiunta di &quot; `/*`&quot; in xpath) (utilizzato solo se &#39; `exact`&#39; non è vero, facoltativo)

* **self**

   esegue la ricerca nella sottostruttura, ma include il nodo di base specificato come percorso (nessun carattere jolly)

### proprietà {#property}

Corrisponde alle proprietà JCR e ai relativi valori.

Supporta l&#39;estrazione dei facet. Fornirà bucket per ogni valore di proprietà univoco nei risultati.

#### Proprietà {#properties-15}

* **proprietà**

   percorso relativo alla proprietà, ad esempio `jcr:title`

* **valore**

   value to check property for; segue il tipo di proprietà JCR in conversioni stringa

* **N_value**

   use `1_value`, `2_value`, ... per controllare più valori (combinati con `OR` per impostazione predefinita, con `AND` if e=true) (da 5.3)

* **e**

   impostato su true per combinare più valori ( `N_value`) con AND (da 5.3)

* **operation**

   &quot; `equals`&quot; per corrispondenza esatta (impostazione predefinita), &quot; `unequals`&quot; per il confronto di uguaglianza, &quot; `like`&quot; per l&#39;utilizzo della funzione `jcr:like` xpath (facoltativo), &quot; `not`&quot; per l&#39;assenza di corrispondenza (ad esempio &quot; `not(@prop)`&quot; in xpath, value param verrà ignorato) o &quot; `exists`&quot; per il controllo dell&#39;esistenza (il valore può essere true - la proprietà deve esistere, il valore predefinito - o falso - uguale a &quot; `not`&quot;)

* **profondità**

   numero di livelli di caratteri jolly al di sotto dei quali può esistere la proprietà/percorso relativo (ad esempio, `property=size depth=2` controllerà nodo/dimensione, nodo/&amp;ast;/dimensione e nodo/&amp;ast;/&amp;ast;/dimensione)

### rangeproperty {#rangeproperty}

Corrisponde a una proprietà JCR rispetto a un intervallo. Ciò si applica alle proprietà con tipi lineari quali `LONG`, `DOUBLE` e `DECIMAL`. Per `DATE` informazioni, consulta il predicato dell’intervallo di date con formato data ottimizzato.

È possibile definire un limite inferiore e un limite superiore o solo uno di essi. Operazione (ad esempio È inoltre possibile specificare &quot;minore di&quot; o &quot;minore o uguale a&quot;) per ciascun limite inferiore e superiore.

Non supporta l&#39;estrazione facet.

#### Proprietà {#properties-16}

* **proprietà**

   percorso relativo alla proprietà

* **lowerBound**

   lower bound to check, proprietà

* **lowerOperation**

   &quot; `>`&quot; (predefinito) o &quot; `>=`&quot;, si applica al `lowerValue`

* **UpperBound**

   limite superiore per controllare la proprietà

* **UpperOperation**

   &quot; `<`&quot; (predefinito) o &quot; `<=`&quot;, si applica al `lowerValue`

* **decimale**

   &quot; `true`&quot; se la proprietà selezionata è di tipo Decimal

### relativedaterange {#relativedaterange}

Corrisponde `JCR DATE` alle proprietà rispetto a un intervallo di data/ora utilizzando gli offset relativi all&#39;ora del server corrente. È possibile specificare `lowerBound` e `upperBound` utilizzare un valore in millisecondi o la sintassi di bugzilla `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni). Prefisso con &quot; `-`&quot; per indicare un offset negativo prima dell&#39;ora corrente. Se si specifica solo `lowerBound` o `upperBound`, l&#39;altro valore predefinito è 0, ovvero l&#39;ora corrente.

Esempio:

* `upperBound=1h` (e no `lowerBound`) seleziona qualsiasi elemento nell&#39;ora successiva
* `lowerBound=-1d` (e no `upperBound`) avrebbe selezionato qualcosa nelle ultime 24 ore
* `lowerBound=-6M` e `upperBound=-3M` sceglierebbe qualcosa dai 6 ai 3 mesi
* `lowerBound=-1500` e `upperBound=5500` avrebbe selezionato qualsiasi cosa tra 1500 millisecondi negli ultimi e 5500 millisecondi nel futuro
* `lowerBound=1d` e `upperBound=2d` sceglierebbe qualsiasi cosa dopo domani

Si noti che non prende in considerazione anni bisestili e che tutti i mesi sono 30 giorni.

Non supporta il filtro.

Supporta l&#39;estrazione dei facet nello stesso modo del predicato daterange.

#### Proprietà {#properties-17}

* **UpperBound**

   data superiore in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora del server corrente, utilizzare &quot;-&quot; per l&#39;offset negativo

* **lowerBound**

   data più bassa in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora corrente del server, utilizzare &quot;-&quot; per l&#39;offset negativo

### root {#root}

Gruppo di predicati radice. Supporta tutte le funzionalità di un gruppo e consente di impostare parametri di query globali.

Il nome &quot;root&quot; non viene mai utilizzato in una query, è implicito.

#### Proprietà {#properties-18}

* **p.offset**

   numero che indica l’inizio della pagina dei risultati, ovvero quanti elementi saltare

* **p.limit**

   numero che indica le dimensioni della pagina

* **p.impressionTotal**

   consigliato: evitare di calcolare l&#39;intero risultato complessivo che può essere costoso; un numero che indica il totale massimo da conteggiare fino a (ad esempio 1000, un numero che dà agli utenti un feedback sufficiente sulla dimensione approssimativa e sui numeri esatti per risultati più piccoli) oppure &quot; `true`&quot; per contare solo fino al minimo necessario `p.offset` + `p.limit`

* **p.excerpt**

   se impostato su &quot; `true`&quot;, includete un estratto di testo completo nel risultato

* **p.hits**

   (solo per il servlet JSON) selezionate il modo in cui gli hit vengono scritti come JSON, con i seguenti standard (estensibili tramite il servizio ResultHitWriter):

   * **semplice**:

      elementi minimi come `path`, `title`, `lastmodified`, `excerpt` (se impostati)

   * **completo**:

      rendering JSON sling del nodo, con `jcr:path` indicazione del percorso dell&#39;hit: per impostazione predefinita elenca solo le proprietà dirette del nodo, include una struttura ad albero più profonda con `p.nodedepth=N`, con 0 che significa l&#39;intera sottostruttura infinita; aggiungere `p.acls=true` per includere le autorizzazioni JCR della sessione corrente sull&#39;elemento risultato dato (mappature: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **selettivo**:

      solo le proprietà specificate in `p.properties`, che è un elenco di percorsi relativi separati da spazi (utilizzate &quot;+&quot; negli URL); se il percorso relativo ha una profondità > 1 questi saranno rappresentati come oggetti secondari; la speciale proprietà jcr:path include il percorso dell&#39;hit

### savedquery {#savedquery}

Include tutti i predicati di una query querybuilder persistente nella query corrente come un predicato di sottogruppo.

Si noti che questo non eseguirà una query supplementare ma estenderà la query corrente.

Le query possono essere persistenti a livello di programmazione utilizzando `QueryBuilder#storeQuery()`. Il formato può essere una proprietà String su più righe o un `nt:file` nodo che contiene la query come file di testo in formato delle proprietà Java.

Non supporta l&#39;estrazione facet per i predicati della query salvata.

#### Proprietà {#properties-19}

* **savedquery**

   percorso della query salvata (proprietà String o `nt:file` nodo)

### similar {#similar}

Ricerca per similarità con JCR XPath `rep:similar()`.

Non supporta il filtro. Non supporta l&#39;estrazione facet.

#### Proprietà {#properties-20}

* **percorso** assoluto simile al nodo per il quale trovare nodi simili

* **local** un percorso relativo a un nodo discendente o `.` per il nodo corrente (facoltativo, il valore predefinito è &quot; `.`&quot;)

### tag {#tag}

Consente di cercare contenuti con tag con uno o più tag, specificando i percorsi del titolo dei tag.

Supporta l&#39;estrazione dei facet. Fornirà bucket per ciascun tag univoco, utilizzando il percorso del titolo del tag corrente.

#### Proprietà {#properties-21}

* **tag**

   percorso titolo tag da cercare, ad esempio &quot;Proprietà risorsa: Orientamento / Orizzontale&quot;

* **N_value**

   use `1_value`, `2_value`, ... per controllare più tag (combinati con `OR` per impostazione predefinita, con `AND` if e=true) (da 5.6)

* **proprietà**

   (o percorso relativo alla proprietà) da esaminare (impostazione predefinita &quot; `cq:tags`&quot;)

### tagid {#tagid}

Consente di cercare contenuti con tag con uno o più tag, specificando ID di tag.

Supporta l&#39;estrazione dei facet. Fornirà bucket per ciascun tag univoco, utilizzando l&#39;ID tag corrente.

#### Proprietà {#properties-22}

* **tagid**

   id tag da cercare, ad esempio &quot; `properties:orientation/landscape`&quot;

* **N_value**

   use `1_value`, `2_value`, ... per verificare la presenza di più tag (combinati con `OR` per impostazione predefinita, con `AND` if e=true) (da 5.6)

* **proprietà**

   (o percorso relativo alla proprietà) da esaminare (impostazione predefinita &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

Consente di ricercare contenuti ai quali sono assegnati uno o più tag, specificando le parole chiave. In questo modo, i tag che contengono queste parole chiave nei loro titoli verranno prima cercati, quindi il risultato verrà limitato solo agli elementi ai quali è stato assegnato il tag.

Non supporta l&#39;estrazione facet.

#### Proprietà {#Properties-1}

* **tagsearch**

   parola chiave da cercare nei titoli dei tag

* **proprietà**

   (o percorso relativo alla proprietà) da esaminare (impostazione predefinita &quot; `cq:tags`&quot;)

* **lang**

   per effettuare ricerche solo in un determinato titolo di tag localizzato (ad esempio &quot; `de`&quot;)

* **all**

   (bool) cercare l’intero testo completo del tag, ad esempio tutti i titoli, la descrizione ecc. (ha la precedenza su &quot;l `ang`&quot;)

### tipo {#type}

Limita i risultati a un tipo di nodo JCR specifico, sia al tipo di nodo principale che al tipo di mixin. Verranno inoltre individuati i sottotipi di tale tipo di nodo. Gli indici di ricerca del repository devono coprire i tipi di nodo per un&#39;esecuzione efficiente.

Supporta l&#39;estrazione dei facet. Forniranno bucket per ogni tipo univoco nei risultati.

#### Proprietà {#Properties-2}

* **tipo**

   tipo di nodo o nome del mixin da cercare, ad esempio `cq:Page`