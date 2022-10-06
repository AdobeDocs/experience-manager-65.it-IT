---
title: Riferimento predicato di Query Builder
seo-title: Query Builder Predicate Reference
description: Riferimento predicato completo per l’API di Query Builder.
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2310'
ht-degree: 3%

---

# Riferimento predicato di Query Builder{#query-builder-predicate-reference}

## Generale {#general}

* [root](#root)
* [gruppo](#group)
* [ordine](#orderby)

## Predicati {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [fulltext](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [language](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [principale](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [MemberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [non scaduto](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [path](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [proprietà](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativa](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [simile](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [tipo](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Corrisponde alle proprietà JCR BOOLEAN. Accetta solo i valori &quot; `true`&quot; e &quot; `false`&quot;. In caso di &quot; `false`&quot;, corrisponde se la proprietà ha il valore &quot; `false`&quot; o se non esiste affatto. Questo può essere utile per verificare la presenza di flag booleani impostati solo quando sono abilitati.

L&#39;ereditato &quot; `operation`&quot; il parametro non ha alcun significato.

Supporta l’estrazione dei facet. Fornirà bucket per ogni `true` o `false` ma solo per le proprietà esistenti.

#### Proprietà {#properties}

* **boolproperty**
percorso relativo alla proprietà, ad esempio 
`myFeatureEnabled` oppure `jcr:content/myFeatureEnabled`

* **value**
valore per la verifica della proprietà, &quot; 
`true`&quot; oppure &quot; `false`&quot;

### contentfragment {#contentfragment}

Limita il risultato ai frammenti di contenuto.

Non supporta il filtro.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-1}

* **contentfragment**
Può essere utilizzato con qualsiasi valore per verificare la presenza di frammenti di contenuto.

### dateComparison {#datecomparison}

Confronta due proprietà JCR DATE tra loro. Può verificare se sono uguali, ineguali, maggiori o maggiori di o uguali.

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca.

#### Proprietà {#properties-2}

* **property1**

   percorso della prima proprietà data

* **property2**

   percorso della proprietà seconda data

* **operation**

   &quot; `equals`&quot; per corrispondenza esatta, &quot; `!=`&quot; per il confronto tra diseguaglianza, &quot; `greater`&quot; per proprietà1 maggiore di proprietà2, &quot; `>=`&quot; per property1 maggiore o uguale a property2. Il valore predefinito è &quot; `equals`&quot;.

### daterange {#daterange}

Corrisponde alle proprietà JCR DATE rispetto a un intervallo di data/ora. Questo utilizza il formato ISO8601 per date e ore ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) e consente anche rappresentazioni parziali, come `YYYY-MM-DD`. In alternativa, la marca temporale può essere fornita come numero di millisecondi a partire dal 1970 nel fuso orario UTC, il formato ora unix.

Puoi cercare qualsiasi elemento tra due marche temporali, più recenti o più vecchie di una data specificata, e puoi anche scegliere tra intervalli inclusivi e aperti.

Supporta l’estrazione dei facet. Fornirà i secchi &quot;oggi&quot;, &quot;questa settimana&quot;, &quot;questo mese&quot;, &quot;ultimi 3 mesi&quot;, &quot;quest&#39;anno&quot;, &quot;l&#39;anno scorso&quot; e &quot;prima dello scorso anno&quot;.

Non supporta il filtro.

#### Proprietà {#properties-3}

* **proprietà**

   percorso relativo a un `DATE` ad esempio `jcr:lastModified`

* **lowerBound**

   data inferiore associata a controllare la proprietà, ad esempio `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (più recente) o &quot; `>=`&quot; (a o più recente), si applica al `lowerBound`. Il valore predefinito è &quot; `>`&quot;.

* **UpperBound**

   limite superiore per controllare la proprietà, ad esempio `2014-10-01T12:15:00`

* **UpperOperation**

   &quot; `<`&quot; (precedente) o &quot; `<=`&quot; (a partire da), si applica al `upperBound`. Il valore predefinito è &quot; `<`&quot;.

* **timeZone**

   ID del fuso orario da utilizzare quando non viene fornito come stringa di data ISO-8601. L’impostazione predefinita è il fuso orario predefinito del sistema.

### excludepaths {#excludepaths}

Esclude i nodi dal risultato quando il loro percorso corrisponde a un&#39;espressione regolare.

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-4}

* **excludepaths**

   espressione regolare confrontata con i percorsi dei risultati, esclusi quelli corrispondenti dal risultato.

### fulltext {#fulltext}

Cerca i termini nell&#39;indice fulltext.

Non supporta il filtro.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-5}

* **fulltext**

   i termini di ricerca a testo intero

* **relPath**

   il percorso relativo da cercare nella proprietà o nel sottonodo. Questa proprietà è facoltativa.

### gruppo {#group}

Consente di creare condizioni nidificate. I gruppi possono contenere gruppi nidificati. Tutto in una query querybuilder è implicitamente in un gruppo root, che può avere `p.or` e `p.not` anche i parametri.

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

Questo cerca il termine &quot;**Gestione**&quot; all&#39;interno delle pagine in `/content/geometrixx/en` o in attività `/content/dam/geometrixx`.

Questo è concettualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Tieni presente che tali join OR necessitano di buoni indici per le prestazioni.

#### Proprietà {#properties-6}

* **p.or**

   se impostato su &quot; `true`&quot;, solo un predicato nel gruppo deve corrispondere. Questo valore predefinito è &quot; `false`&quot;, ovvero tutti devono corrispondere

* **p.not**

   se impostato su &quot; `true`&quot;, nega il gruppo (impostazione predefinita &quot; `false`&quot;)

* **&lt;predicate>**

   aggiunge predicati nidificati

* **N_&lt;predicate>**

   aggiunge più predicati nidificati della stessa volta, come `1_property, 2_property, ...`

### hasPermission {#haspermission}

Limita il risultato agli elementi in cui la sessione corrente ha specificato [Privilegi JCR.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-7}

* **hasPermission**

   privilegi JCR separati da virgole che la sessione utente corrente deve avere ALL per il nodo in questione; per esempio `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Trova le pagine CQ in una lingua specifica. Osserva sia la proprietà della lingua della pagina che il percorso della pagina, che spesso include la lingua o le impostazioni internazionali in una struttura del sito di primo livello.

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca.

Supporta l’estrazione dei facet. Fornirà bucket per ogni codice di lingua univoco.

#### Proprietà {#properties-8}

* **language**

   Codice della lingua ISO, ad esempio &quot; `de`&quot;

### principale {#mainasset}

Controlla se un nodo è una risorsa principale DAM e non una risorsa secondaria. Questo è fondamentalmente ogni nodo non all&#39;interno di un nodo &quot;subassets&quot;. Tieni presente che questo non controlla la `dam:Asset` tipo di nodo. Per utilizzare questo predicato, imposta semplicemente &quot; `mainasset=true`&quot; o &quot; `mainasset=false`&quot;, non ci sono ulteriori proprietà.

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca.

Supporta l’estrazione dei facet. Fornirà 2 bucket per le risorse principali e secondarie.

#### Proprietà {#properties-9}

* **principale**

   booleano, &quot; `true`&quot; per le attività principali, &quot; `false`&quot; per le sotto attività

### MemberOf {#memberof}

Trova gli elementi membri di un [raccolta di risorse sling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-10}

* **MemberOf**

   percorso della raccolta di risorse Sling

### nodename {#nodename}

Corrisponde ai nomi dei nodi JCR.

Supporta l’estrazione dei facet. Fornirà bucket per ogni nome di nodo univoco (nome del file).

#### Proprietà {#properties-11}

* **nodename**

   pattern di nome del nodo che consente l’utilizzo di caratteri jolly: `*` = qualsiasi o nessun carattere, `?` = qualsiasi carattere, `[abc]` = solo caratteri tra parentesi

### non scaduto {#notexpired}

Corrisponde agli elementi controllando se una proprietà JCR DATE è maggiore o uguale all&#39;ora del server corrente. Può essere utilizzato per controllare un &quot; `expiresAt`&quot; piace la proprietà date e limita a solo quelli che non sono ancora scaduti ( `notexpired=true`) o che sono già scaduti ( `notexpired=false`).

Non supporta il filtro.

Supporta l’estrazione dei facet nello stesso modo del predicato daterange.

#### Proprietà {#properties-12}

* **non scaduto**

   booleano, &quot; `true`&quot; per non ancora scaduto (data in futuro o uguale), &quot; `false`&quot; per scaduto (data passata) (obbligatorio)

* **proprietà**

   percorso relativo `DATE` proprietà da controllare (obbligatorio)

### ordine {#orderby}

Consente di ordinare il risultato. Se l’ordinamento è richiesto da più proprietà, questo predicato deve essere aggiunto più volte utilizzando il prefisso del numero, ad esempio `1_orderby=first`, `2_oderby=second`.

#### Proprietà {#properties-13}

* **ordine**

   nome della proprietà JCR indicato da una @ iniziale, ad esempio `@jcr:lastModified` o `@jcr:content/jcr:title`, o un altro predicato nella query, ad esempio `2_property`, su cui ordinare

* **ordina**

   ordina direzione, o &quot; `desc`&quot; per discendente o &quot; `asc`&quot; per crescente (predefinito)

* **caso**

   se impostato su &quot; `ignore`&quot; farà distinzione tra maiuscole e minuscole, il che significa che &quot;a&quot; precede &quot;B&quot;; se vuoto o escluso, l&#39;ordinamento è sensibile a maiuscole e minuscole, ovvero &quot;B&quot; precede &quot;a&quot;

### path {#path}

Esegue la ricerca all&#39;interno di un determinato percorso.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-14}

* **path**

   modello di percorso; a seconda dell’esatto, l’intero sottoalbero corrisponderà (come l’aggiunta `//*` in xpath, ma nota che questo non include il percorso base) (esatto=false, predefinito) o solo un percorso esatto corrisponde, che può includere caratteri jolly ( `*`); se è impostato su se stesso, verrà eseguita la ricerca dell&#39;intero sottoalbero, incluso il nodo base

* **esatto**

   if `exact` è true/on, il percorso esatto deve corrispondere, ma può contenere caratteri jolly semplici ( `*`), che corrispondono ai nomi, ma non &quot; `/`&quot;; se è false (predefinito), sono inclusi tutti i discendenti (facoltativo)

* **piatto**

   cerca solo gli elementi figlio diretti (come aggiungere &quot; `/*`&quot; in xpath) (utilizzato solo se &#39; `exact`&#39; non è true, facoltativo)

* **self**

   cerca la sottostruttura ma include il nodo base specificato come percorso (nessun carattere jolly)

### proprietà {#property}

Corrisponde alle proprietà JCR e ai loro valori.

Supporta l’estrazione dei facet. Fornirà bucket per ogni valore di proprietà univoco nei risultati.

#### Proprietà {#properties-15}

* **proprietà**

   percorso relativo alla proprietà, ad esempio `jcr:title`

* **valore**

   valore da controllare per la proprietà; segue il tipo di proprietà JCR in conversioni stringa

* **N_value**

   use `1_value`, `2_value`, ... per controllare più valori (combinati con `OR` per impostazione predefinita, con `AND` if and=true) (a partire da 5.3)

* **e**

   impostato su true per combinare più valori ( `N_value`) con AND (da 5.3)

* **funzionamento**

   &quot;`equals`&quot; per corrispondenza esatta (predefinito), &quot; `unequals`&quot; per il confronto tra diseguaglianza, &quot; `like`&quot; per utilizzare `jcr:like` funzione xpath (opzionale), &quot; `not`&quot; per nessuna corrispondenza (ad esempio &quot;`not(@prop)`&quot; in xpath, il parametro del valore verrà ignorato) o &quot; `exists`&quot; per il controllo dell&#39;esistenza (il valore può essere true - la proprietà deve esistere, il valore predefinito - o falso - è uguale a &quot; `not`&quot;)

* **profondità**

   numero di livelli di caratteri jolly al di sotto dei quali può esistere la proprietà/percorso relativo (ad esempio, `property=size depth=2` controllerà nodo/dimensione, nodo/&amp;ast;/dimensione e nodo/&amp;ast;/&amp;ast;/size)

### rangeproperty {#rangeproperty}

Corrisponde a una proprietà JCR rispetto a un intervallo. Questo vale per le proprietà con tipi lineari quali `LONG`, `DOUBLE` e `DECIMAL`. Per `DATE` consulta il predicato daterange che ha ottimizzato l’input del formato data.

È possibile definire un limite inferiore e un limite superiore o solo uno di essi. Operazione (ad esempio È inoltre possibile specificare &quot;minore di&quot; o &quot;minore o uguale a&quot;) per ciascun limite inferiore e superiore.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-16}

* **proprietà**

   percorso relativo alla proprietà

* **lowerBound**

   limite inferiore per controllare la proprietà

* **lowerOperation**

   &quot; `>`&quot; (predefinito) o &quot; `>=`&quot;, si applica al `lowerValue`

* **UpperBound**

   limite superiore per controllare la proprietà per

* **UpperOperation**

   &quot; `<`&quot; (predefinito) o &quot; `<=`&quot;, si applica al `lowerValue`

* **decimale**

   &quot; `true`&quot; se la proprietà selezionata è di tipo Decimal

### relativa {#relativedaterange}

Corrisponde `JCR DATE` proprietà rispetto a un intervallo data/ora che utilizza scostamenti di tempo relativi all&#39;ora del server corrente. Puoi specificare `lowerBound` e `upperBound` utilizzando un valore di millisecondi o la sintassi di bugzilla `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni). Prefisso con &quot; `-`&quot; per indicare un offset negativo prima dell&#39;ora corrente. Se specifichi solo `lowerBound` o `upperBound`, l’altro valore predefinito è 0, ovvero l’ora corrente.

Esempio:

* `upperBound=1h` (e no) `lowerBound`) seleziona qualsiasi elemento nell’ora successiva
* `lowerBound=-1d` (e no) `upperBound`) seleziona qualsiasi elemento nelle ultime 24 ore
* `lowerBound=-6M` e `upperBound=-3M` seleziona qualcosa dai 6 mesi ai 3 mesi
* `lowerBound=-1500` e `upperBound=5500` seleziona un valore compreso tra 1500 millisecondi nel passato e 5500 millisecondi nel futuro
* `lowerBound=1d` e `upperBound=2d` sceglierei qualsiasi cosa nel giorno dopo domani

Si noti che non prende in considerazione anni bisestili e tutti i mesi sono 30 giorni.

Non supporta il filtro.

Supporta l’estrazione dei facet nello stesso modo del predicato daterange.

#### Proprietà {#properties-17}

* **UpperBound**

   data superiore in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora del server corrente, utilizzare &quot;-&quot; per offset negativo

* **lowerBound**

   data inferiore associata in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora del server corrente, utilizzare &quot;-&quot; per offset negativo

### root {#root}

Gruppo predicato radice. Supporta tutte le funzionalità di un gruppo e consente di impostare parametri di query globali.

Il nome &quot;root&quot; non viene mai utilizzato in una query, è implicito.

#### Proprietà {#properties-18}

* **p.offset**

   numero che indica l’inizio della pagina dei risultati, ovvero quanti elementi ignorare

* **p.limit**

   numero che indica la dimensione della pagina

* **p.guessTotal**

   consigliato: evitare di calcolare il totale del risultato complessivo che può essere costoso; un numero che indica il totale massimo da contare fino a (ad esempio 1000, un numero che fornisce agli utenti un feedback sufficiente sulle dimensioni approssimative e sui numeri esatti per risultati più piccoli) o &quot; `true`&quot; per contare solo fino al minimo necessario `p.offset` + `p.limit`

* **p.excerpt**

   se impostato su &quot; `true`&quot;, includere un estratto di testo completo nel risultato

* **p.hits**

   (solo per il servlet JSON) seleziona il modo in cui gli hit vengono scritti come JSON, con quelli standard (estensibili tramite il servizio ResultHitWriter):

   * **semplice**:

      elementi minimi come `path`, `title`, `lastmodified`, `excerpt` (se impostato)

   * **completo**:

      rendering JSON sling del nodo, con `jcr:path` indica il percorso dell&#39;hit: per impostazione predefinita elenca solo le proprietà dirette del nodo, includi una struttura più profonda con `p.nodedepth=N`, con 0 che significa l&#39;intero sottoalbero infinito; add `p.acls=true` per includere le autorizzazioni JCR della sessione corrente sull&#39;elemento risultato dato (mappature: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **selettivo**:

      solo le proprietà specificate in `p.properties`, che è un elenco di percorsi relativi separati da spazi (usa &quot;+&quot; negli URL); se il percorso relativo ha una profondità > 1, questi saranno rappresentati come oggetti secondari; la speciale proprietà jcr:path include il percorso dell&#39;hit

### savedquery {#savedquery}

Include tutti i predicati di una query querybuilder persistente nella query corrente come predicato di sottogruppo.

Tieni presente che questa operazione non esegue una query aggiuntiva ma estende la query corrente.

Le query possono essere mantenute a livello di programmazione utilizzando `QueryBuilder#storeQuery()`. Il formato può essere una proprietà String su più righe o un `nt:file` nodo che contiene la query come file di testo in formato proprietà Java.

Non supporta l’estrazione dei facet per i predicati della query salvata.

#### Proprietà {#properties-19}

* **savedquery**

   percorso della query salvata (proprietà String o `nt:file` nodo)

### simile {#similar}

Ricerca per similarità con JCR XPath `rep:similar()`.

Non supporta il filtro. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-20}

* **simile**
percorso assoluto del nodo per il quale trovare nodi simili

* **locale**
un percorso relativo a un nodo discendente o 
`.` per il nodo corrente (facoltativo, il valore predefinito è &quot; `.`&quot;)

### tag {#tag}

Cerca il contenuto con tag di uno o più tag, specificando i percorsi del titolo del tag.

Supporta l’estrazione dei facet. Fornirà bucket per ogni tag univoco, utilizzando il percorso del titolo del tag corrente.

#### Proprietà {#properties-21}

* **tag**

   percorso del titolo del tag da cercare, ad esempio &quot;Proprietà risorsa : Orientamento / Orizzontale&quot;

* **N_value**

   use `1_value`, `2_value`, ... per controllare più tag (combinati con `OR` per impostazione predefinita, con `AND` if e=true) (a partire da 5.6)

* **proprietà**

   proprietà (o percorso relativo alla proprietà) da esaminare (impostazione predefinita &quot; `cq:tags`&quot;)

### tagid {#tagid}

Cerca il contenuto con tag di uno o più tag, specificando ID tag.

Supporta l’estrazione dei facet. Fornirà bucket per ogni tag univoco utilizzando il loro ID tag corrente.

#### Proprietà {#properties-22}

* **tagid**

   ID tag da cercare, ad esempio &quot; `properties:orientation/landscape`&quot;

* **N_value**

   use `1_value`, `2_value`, ... per controllare più tagidi (combinati con `OR` per impostazione predefinita, con `AND` if e=true) (a partire da 5.6)

* **proprietà**

   proprietà (o percorso relativo alla proprietà) da esaminare (impostazione predefinita &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

Cerca il contenuto con tag di uno o più tag, specificando le parole chiave. In questo modo verrà innanzitutto eseguita la ricerca di tag contenenti queste parole chiave nei loro titoli, quindi il risultato verrà limitato solo agli elementi con tag.

Non supporta l’estrazione dei facet.

#### Proprietà {#Properties-1}

* **tagsearch**

   parola chiave da cercare nei titoli dei tag

* **proprietà**

   proprietà (o percorso relativo alla proprietà) da esaminare (impostazione predefinita &quot; `cq:tags`&quot;)

* **lang**

   per cercare solo un titolo di tag localizzato (ad es. &quot; `de`&quot;)

* **all**

   (bool) cerca l&#39;intero tag fulltext, cioè tutti i titoli, la descrizione, ecc. (ha la precedenza su &quot;l `ang`&quot;)

### tipo {#type}

Limita i risultati a un tipo di nodo JCR specifico, sia il tipo di nodo principale che il tipo di mixin. Verranno inoltre trovati sottotipi di quel tipo di nodo. Gli indici di ricerca del repository devono coprire i tipi di nodo per un&#39;esecuzione efficiente.

Supporta l’estrazione dei facet. Fornirà bucket per ogni tipo univoco nei risultati.

#### Proprietà {#Properties-2}

* **tipo**

   tipo di nodo o nome mixin da cercare, ad esempio `cq:Page`
