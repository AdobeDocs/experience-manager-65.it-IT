---
title: Riferimento predicato di Query Builder
seo-title: Query Builder Predicate Reference
description: Riferimento predicato completo per l’API Query Builder.
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: f97eb2e028263016131b0c86be5a0508ae4def9b
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 3%

---

# Riferimento predicato di Query Builder{#query-builder-predicate-reference}

>[!CAUTION]
>
>Le informazioni su questa pagina non sono esaustive.
>
>Per informazioni complete, consulta l’elenco in **Predicati disponibili** nella console Debugger di Query Builder; ad esempio, in:
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>Ad esempio, consulta:
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)


## Generale {#general}

* [radice](#root)
* [gruppo](#group)
* [orderby](#orderby)

## Predicati {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [intervallo di date](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [full-text](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [lingua](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [risorsa principale](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [non scaduto](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [percorso](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [proprietà](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [simile](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [tipo](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Corrisponde alle proprietà BOOLEAN di JCR. Accetta solo i valori &quot;. `true`&quot; e &quot; `false`&quot;. Nel caso di &quot; `false`&quot;, corrisponderà se la proprietà ha il valore &quot; `false`&quot; o se non esiste affatto. Questo può essere utile per verificare la presenza di flag booleani impostati solo se attivati.

L’ ereditato &quot; `operation`Il parametro &quot; non ha alcun significato.

Supporta l&#39;estrazione dei facet. Fornirà bucket per ogni `true` o `false` ma solo per le proprietà esistenti.

#### Proprietà {#properties}

* **boolproperty**
percorso relativo della proprietà, ad esempio 
`myFeatureEnabled` oppure `jcr:content/myFeatureEnabled`

* **valore**
valore per cui verificare la proprietà, &quot; 
`true`&quot; oppure &quot; `false`&quot;

### contentfragment {#contentfragment}

Limita il risultato ai frammenti di contenuto.

Filtro non supportato.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-1}

* **contentfragment**
Può essere utilizzato con qualsiasi valore per verificare la presenza di frammenti di contenuto.

### dateComparison {#datecomparison}

Confronta due proprietà DATA JCR tra loro. Può verificare se sono uguali, ineguali, maggiori o maggiori o uguali.

Si tratta di un predicato di solo filtro e non può sfruttare un indice di ricerca.

#### Proprietà {#properties-2}

* **property1**

   percorso della prima proprietà data

* **property2**

   percorso della seconda proprietà data

* **operazione**

   &quot; `equals`&quot; per corrispondenza esatta, &quot; `!=`&quot; per il confronto della disuguaglianza, &quot; `greater`&quot; per property1 maggiore di property2, &quot; `>=`&quot; per property1 maggiore o uguale a property2. Il valore predefinito è &quot; `equals`&quot;.

### intervallo di date {#daterange}

Confronta le proprietà DATA JCR con un intervallo di data/ora. Utilizza il formato ISO8601 per data e ora ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) e consente anche rappresentazioni parziali, come `YYYY-MM-DD`. In alternativa, la marca temporale può essere fornita come numero di millisecondi dal 1970 nel fuso orario UTC, il formato di ora unix.

Puoi cercare qualsiasi cosa tra due marche temporali, qualsiasi cosa più recente o più vecchia di una determinata data e anche scegliere tra intervalli inclusivi e aperti.

Supporta l&#39;estrazione dei facet. Saranno forniti bucket &quot;oggi&quot;, &quot;questa settimana&quot;, &quot;questo mese&quot;, &quot;ultimi 3 mesi&quot;, &quot;quest’anno&quot;, &quot;ultimo anno&quot; e &quot;prima dello scorso anno&quot;.

Filtro non supportato.

#### Proprietà {#properties-3}

* **proprietà**

   percorso relativo di un `DATE` proprietà, ad esempio `jcr:lastModified`

* **lowerBound**

   data inferiore associata per verificare la proprietà, ad esempio `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (più recente) o &quot; `>=`&quot; (uguale o successivo), si applica al `lowerBound`. Il valore predefinito è &quot; `>`&quot;.

* **upperBound**

   limite superiore per verificare la proprietà, ad esempio `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (precedente) o &quot; `<=`&quot; (precedente o uguale a), si applica al `upperBound`. Il valore predefinito è &quot; `<`&quot;.

* **fuso orario**

   ID del fuso orario da utilizzare quando non è specificato come stringa di data ISO-8601. Il fuso orario predefinito è quello del sistema.

### excludepaths {#excludepaths}

Esclude i nodi dal risultato in cui il loro percorso corrisponde a un’espressione regolare.

Si tratta di un predicato di solo filtro e non può sfruttare un indice di ricerca.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-4}

* **excludepaths**

   espressione regolare confrontata con i percorsi dei risultati, escludendo quelli corrispondenti dal risultato.

### full-text {#fulltext}

Cerca i termini nell&#39;indice full-text.

Filtro non supportato.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-5}

* **full-text**

   termini di ricerca full-text

* **relPath**

   percorso relativo per la ricerca nella proprietà o nel sottonodo. Questa proprietà è facoltativa.

### gruppo {#group}

Consente di creare condizioni nidificate. I gruppi possono contenere gruppi nidificati. Tutto ciò che si trova in una query querybuilder si trova implicitamente in un gruppo radice, che può avere `p.or` e `p.not` parametri.

Esempio per associare una delle due proprietà a un valore:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Concettualmente `(1_property` OPPURE `2_property)`.

Esempio di gruppi nidificati:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Questo cerca il termine &quot;**Gestione**&quot; nelle pagine di `/content/geometrixx/en` o in risorse in `/content/dam/geometrixx`.

Concettualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Tieni presente che tali join OR richiedono indici validi per le prestazioni.

#### Proprietà {#properties-6}

* **p.or**

   se impostato su &quot; `true`&quot;, solo un predicato nel gruppo deve corrispondere. Il valore predefinito è &quot; `false`&quot;, il che significa che tutti devono corrispondere

* **p.not**

   se impostato su &quot; `true`&quot;, ignora il gruppo (impostazione predefinita: &quot; `false`&quot;)

* **&lt;predicate>**

   aggiunge predicati nidificati

* **N_&lt;predicate>**

   aggiunge più predicati nidificati dello stesso tempo, come `1_property, 2_property, ...`

### hasPermission {#haspermission}

Limita il risultato agli elementi in cui la sessione corrente ha il valore specificato [Privilegi JCR.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Si tratta di un predicato di solo filtro e non può sfruttare un indice di ricerca. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-7}

* **hasPermission**

   privilegi JCR separati da virgole che la sessione utente corrente deve avere TUTTI per il nodo in questione; ad esempio `jcr:write`, `jcr:modifyAccessControl`

### lingua {#language}

Trova le pagine CQ in una lingua specifica. Vengono esaminate sia la proprietà lingua della pagina che il percorso della pagina, che spesso include la lingua o le impostazioni locali in una struttura del sito principale.

Si tratta di un predicato di solo filtro e non può sfruttare un indice di ricerca.

Supporta l&#39;estrazione dei facet. Fornirà bucket per ogni codice lingua univoco.

#### Proprietà {#properties-8}

* **lingua**

   Codice della lingua ISO, ad esempio &quot; `de`&quot;

### risorsa principale {#mainasset}

Controlla se un nodo è una risorsa principale DAM e non una risorsa secondaria. In pratica, si tratta di ogni nodo non incluso in un nodo &quot;risorse secondarie&quot;. Tieni presente che questa operazione non verifica la presenza di `dam:Asset` tipo di nodo. Per utilizzare questo predicato, imposta semplicemente &quot; `mainasset=true`&quot; o &quot; `mainasset=false`&quot;, non sono presenti ulteriori proprietà.

Si tratta di un predicato di solo filtro e non può sfruttare un indice di ricerca.

Supporta l&#39;estrazione dei facet. Fornirà 2 bucket per le risorse principali e secondarie.

#### Proprietà {#properties-9}

* **risorsa principale**

   booleano, &quot; `true`&quot; per le risorse principali, &quot; `false`&quot; per risorse secondarie

### memberOf {#memberof}

Trova gli elementi che sono membri di un [raccolta di risorse sling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Si tratta di un predicato di solo filtro e non può sfruttare un indice di ricerca. Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-10}

* **memberOf**

   percorso della raccolta di risorse Sling

### nodename {#nodename}

Corrisponde ai nomi dei nodi JCR.

Supporta l&#39;estrazione dei facet. Fornirà i bucket per ogni nome di nodo univoco (nome file).

#### Proprietà {#properties-11}

* **nodename**

   pattern del nome del nodo che consente l’utilizzo di caratteri jolly: `*` = qualsiasi carattere o nessun carattere, `?` = qualsiasi carattere, `[abc]` = solo caratteri tra parentesi

### non scaduto {#notexpired}

Corrisponde agli elementi controllando se una proprietà DATA JCR è maggiore o uguale all’ora corrente del server. Può essere utilizzato per controllare un’&quot; `expiresAt`&quot; piace la proprietà data e limita a quelle che non sono ancora scadute ( `notexpired=true`) o che sono già scaduti ( `notexpired=false`).

Filtro non supportato.

Supporta l&#39;estrazione di facet nello stesso modo del predicato dell&#39;intervallo di dati.

#### Proprietà {#properties-12}

* **non scaduto**

   booleano, &quot; `true`&quot; per non ancora scaduto (data futura o uguale), &quot; `false`&quot; per scaduto (data nel passato) (obbligatorio)

* **proprietà**

   percorso relativo del `DATE` proprietà da verificare (obbligatoria)

### orderby {#orderby}

Consente di ordinare il risultato. Se è necessario ordinare per più proprietà, questo predicato deve essere aggiunto più volte utilizzando il prefisso numerico, ad esempio `1_orderby=first`, `2_oderby=second`.

#### Proprietà {#properties-13}

* **orderby**

   il nome della proprietà JCR indicato da una @ iniziale, ad esempio `@jcr:lastModified` o `@jcr:content/jcr:title`, o un altro predicato nella query, ad esempio `2_property`, su cui ordinare

* **ordina**

   direzione di ordinamento, scegliendo tra &quot; `desc`&quot; per decrescente o &quot; `asc`&quot; per crescente (impostazione predefinita)

* **caso**

   se impostato su &quot; `ignore`&quot; non distingue tra maiuscole e minuscole, ovvero &quot;a&quot; precede &quot;B&quot;; se vuoto o non specificato, l&#39;ordinamento distingue tra maiuscole e minuscole, ovvero &quot;B&quot; precede &quot;a&quot;

### percorso {#path}

Esegue ricerche all&#39;interno di un determinato percorso.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-14}

* **percorso**

   pattern di tracciato; a seconda dell’esatto, l’intera sottostruttura corrisponderà (ad esempio, aggiungendo `//*` in xpath, ma tieni presente che non include il percorso di base) (exact=false, default) o solo una corrispondenza esatta del percorso, che può includere caratteri jolly ( `*`); se è impostato self, verrà eseguita la ricerca nell&#39;intera sottostruttura, incluso il nodo di base

* **esatto**

   se `exact` è true/on, il percorso esatto deve corrispondere, ma può contenere caratteri jolly semplici ( `*`), che corrispondono ai nomi, ma non &quot; `/`&quot;; se è false (impostazione predefinita), tutti i discendenti sono inclusi (facoltativo)

* **piatto**

   cerca solo gli elementi secondari diretti (ad esempio, aggiungendo &quot; `/*`&quot; in xpath) (utilizzato solo se &quot; `exact`&#39; non è true, facoltativo)

* **self**

   esegue la ricerca nella sottostruttura ma include il nodo di base indicato come percorso (nessun carattere jolly)

### proprietà {#property}

Corrisponde alle proprietà JCR e ai relativi valori.

Supporta l&#39;estrazione dei facet. Fornirà dei bucket per ogni valore di proprietà univoco nei risultati.

#### Proprietà {#properties-15}

* **proprietà**

   percorso relativo della proprietà, ad esempio `jcr:title`

* **valore**

   valore di cui controllare la proprietà; segue il tipo di proprietà JCR per le conversioni stringa

* **N_value**

   utilizzare `1_value`, `2_value`, ... per verificare la presenza di più valori (combinati con `OR` per impostazione predefinita, con `AND` if and=true) (dal punto 5.3)

* **e**

   impostato su true per combinare più valori ( `N_value`) con E (da 5.3)

* **operazione**

   &quot;`equals`&quot; per corrispondenza esatta (impostazione predefinita), &quot; `unequals`&quot; per il confronto della disuguaglianza, &quot; `like`&quot; per l’utilizzo di `jcr:like` funzione xpath (opzionale), &quot; `not`&quot; senza corrispondenza (es. &quot;`not(@prop)`&quot; in xpath, il parametro value verrà ignorato) o &quot; `exists`&quot; per il controllo dell’esistenza (il valore può essere true - la proprietà deve esistere, il valore predefinito - o false - è uguale a &quot; `not`&quot;)

* **profondità**

   numero di livelli di caratteri jolly sotto i quali può esistere la proprietà o il percorso relativo (ad esempio, `property=size depth=2` controllerà node/size, node/&amp;ast;/size e node/&amp;ast;/&amp;ast;/size)

### rangeproperty {#rangeproperty}

Corrisponde a una proprietà JCR rispetto a un intervallo. Questo vale per le proprietà con tipi lineari come `LONG`, `DOUBLE` e `DECIMAL`. Per `DATE` consulta il predicato daterange con input in formato data ottimizzato.

È possibile definire un limite inferiore e un limite superiore o solo uno di essi. L&#39;operazione (p. es. &quot;lesser than&quot; (minore di) o &quot;lesser or equals&quot; (minore o uguale a)) può essere specificato anche per il limite inferiore e superiore singolarmente.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-16}

* **proprietà**

   percorso relativo della proprietà

* **lowerBound**

   limite inferiore per verificare la proprietà per

* **lowerOperation**

   &quot; `>`&quot; (impostazione predefinita) o &quot; `>=`&quot;, si applica al `lowerValue`

* **upperBound**

   limite superiore per verificare la proprietà per

* **upperOperation**

   &quot; `<`&quot; (impostazione predefinita) o &quot; `<=`&quot;, si applica al `lowerValue`

* **decimale**

   &quot; `true`&quot; se la proprietà selezionata è di tipo Decimal

### relativedaterange {#relativedaterange}

Corrisponde a `JCR DATE` proprietà rispetto a un intervallo di data/ora utilizzando gli offset temporali relativi all&#39;ora corrente del server. È possibile specificare `lowerBound` e `upperBound` utilizzando un valore in millisecondi o la sintassi bugzilla `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) Prefisso con &quot; `-`&quot; per indicare un offset negativo prima dell&#39;ora corrente. Se si specifica solo `lowerBound` o `upperBound`, l’altro assumerà come valore predefinito 0, che indica l’ora corrente.

Ad esempio:

* `upperBound=1h` (e no `lowerBound`) avrebbe selezionato qualsiasi cosa nell&#39;ora successiva
* `lowerBound=-1d` (e no `upperBound`) avrebbe selezionato qualsiasi cosa nelle ultime 24 ore
* `lowerBound=-6M` e `upperBound=-3M` sceglierebbe qualsiasi prodotto di età compresa tra 6 e 3 mesi
* `lowerBound=-1500` e `upperBound=5500` consente di selezionare un valore compreso tra 1500 millisecondi nel passato e 5500 millisecondi nel futuro
* `lowerBound=1d` e `upperBound=2d` avrebbe selezionato qualsiasi cosa nel dopodomani

Si noti che non prende in considerazione anni bisestili e tutti i mesi sono 30 giorni.

Filtro non supportato.

Supporta l&#39;estrazione di facet nello stesso modo del predicato dell&#39;intervallo di dati.

#### Proprietà {#properties-17}

* **upperBound**

   limite superiore di date in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora corrente del server, utilizzare &quot;-&quot; per l&#39;offset negativo

* **lowerBound**

   limite di data inferiore in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora corrente del server, utilizzare &quot;-&quot; per l&#39;offset negativo

### radice {#root}

Gruppo di predicati radice. Supporta tutte le funzioni di un gruppo e consente di impostare i parametri di query globali.

Il nome &quot;root&quot; non viene mai utilizzato in una query, è implicito.

#### Proprietà {#properties-18}

* **p.offset**

   numero che indica l&#39;inizio della pagina dei risultati, ovvero il numero di elementi da saltare

* **p.limit**

   numero che indica le dimensioni della pagina

* **p.guessTotal**

   consigliato: evita di calcolare il totale completo dei risultati che può essere costoso; o un numero che indica il totale massimo da contare fino a (ad esempio 1000, un numero che fornisce agli utenti un feedback sufficiente sulle dimensioni approssimative e i numeri esatti per risultati più piccoli) o &quot; `true`&quot; per contare solo il minimo necessario `p.offset` + `p.limit`

* **p.estratto**

   se impostato su &quot; `true`&quot;, includi estratto di testo completo nel risultato

* **p.hits**

   (solo per il servlet JSON) seleziona il modo in cui gli hit vengono scritti come JSON, con questi standard (estensibili tramite il servizio ResultHitWriter):

   * **semplice**:

      elementi minimi come `path`, `title`, `lastmodified`, `excerpt` (se impostato)

   * **completo**:

      rendering Sling JSON del nodo, con `jcr:path` che indica il percorso dell’hit: per impostazione predefinita elenca solo le proprietà dirette del nodo, include una struttura ad albero più profonda con `p.nodedepth=N`, dove 0 indica l&#39;intero sottoalbero infinito; aggiungere `p.acls=true` per includere le autorizzazioni JCR della sessione corrente sull’elemento risultato specificato (mappature: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **selettivo**:

      solo le proprietà specificate in `p.properties`, che è un elenco di percorsi relativi separato da spazi (negli URL utilizzare &quot;+&quot;); se il percorso relativo ha una profondità > 1, questi verranno rappresentati come oggetti secondari; la speciale proprietà jcr:path include il percorso dell’hit

### savedquery {#savedquery}

Include tutti i predicati di una query querybuilder persistente nella query corrente come predicato di sottogruppo.

Tieni presente che non verrà eseguita una query aggiuntiva, ma verrà estesa la query corrente.

Le query possono essere rese persistenti a livello di programmazione utilizzando `QueryBuilder#storeQuery()`. Il formato può essere una proprietà String su più righe o una proprietà `nt:file` nodo che contiene la query come file di testo in formato proprietà Java.

Non supporta l’estrazione dei facet per i predicati della query salvata.

#### Proprietà {#properties-19}

* **savedquery**

   percorso della query salvata (proprietà String o `nt:file` node)

### simile {#similar}

Ricerca per affinità utilizzando JCR XPath `rep:similar()`.

Filtro non supportato. Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-20}

* **simile**
percorso assoluto del nodo per il quale trovare nodi simili

* **locale**
un percorso relativo a un nodo discendente oppure 
`.` per il nodo corrente (facoltativo, il valore predefinito è &quot;) `.`&quot;)

### tag {#tag}

Cerca il contenuto con uno o più tag, specificando i percorsi dei titoli dei tag.

Supporta l&#39;estrazione dei facet. Fornirà dei bucket per ogni tag univoco, utilizzando il percorso del titolo del tag corrente.

#### Proprietà {#properties-21}

* **tag**

   percorso del titolo del tag da cercare, ad esempio &quot;Proprietà risorsa: orientamento / Orizzontale&quot;

* **N_value**

   utilizzare `1_value`, `2_value`, ... per verificare la presenza di più tag (combinati con `OR` per impostazione predefinita, con `AND` if and=true) (dal 5.6)

* **proprietà**

   (o il percorso relativo della proprietà) (impostazione predefinita &quot; `cq:tags`&quot;)

### tagid {#tagid}

Cerca il contenuto con uno o più tag, specificando gli ID tag.

Supporta l&#39;estrazione dei facet. Fornirà dei bucket per ogni tag univoco, utilizzando il relativo ID tag corrente.

#### Proprietà {#properties-22}

* **tagid**

   id tag da cercare, ad esempio &quot; `properties:orientation/landscape`&quot;

* **N_value**

   utilizzare `1_value`, `2_value`, ... per verificare la presenza di più tag (combinati con `OR` per impostazione predefinita, con `AND` if and=true) (dal 5.6)

* **proprietà**

   (o il percorso relativo della proprietà) (impostazione predefinita &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

Cerca il contenuto con uno o più tag, specificando le parole chiave. In questo modo verranno innanzitutto cercati i tag che contengono queste parole chiave nei titoli, quindi verranno limitati solo gli elementi con queste parole chiave.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#Properties-1}

* **tagsearch**

   parola chiave da cercare nei titoli dei tag

* **proprietà**

   (o il percorso relativo della proprietà) (impostazione predefinita &quot; `cq:tags`&quot;)

* **lang**

   per eseguire ricerche solo in un determinato titolo di tag localizzato (ad esempio, &quot; `de`&quot;)

* **tutti**

   (bool) cerca l’intero testo completo del tag, ovvero tutti i titoli, la descrizione, ecc. (ha la precedenza su &quot;l `ang`&quot;)

### tipo {#type}

Limita i risultati a un tipo di nodo JCR specifico, sia di tipo di nodo principale che mixin. Verranno trovati anche i sottotipi di quel tipo di nodo. Tieni presente che gli indici di ricerca dell’archivio devono coprire i tipi di nodo per un’esecuzione efficiente.

Supporta l&#39;estrazione dei facet. Fornirà dei bucket per ogni tipo univoco nei risultati.

#### Proprietà {#Properties-2}

* **tipo**

   tipo di nodo o nome mixin da cercare, ad esempio `cq:Page`
