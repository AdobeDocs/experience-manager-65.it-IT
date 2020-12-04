---
title: Sviluppo di report
seo-title: Sviluppo di report
description: AEM fornisce una selezione di report standard basati su un framework di reporting
seo-description: AEM fornisce una selezione di report standard basati su un framework di reporting
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
translation-type: tm+mt
source-git-commit: ea6da2b75cce4052211fb8f0793f1f380eb85a20
workflow-type: tm+mt
source-wordcount: '5252'
ht-degree: 0%

---


# Sviluppo di report{#developing-reports}

AEM fornisce una selezione di [report standard](/help/sites-administering/reporting.md) la maggior parte dei quali sono basati su un framework di reporting.

Utilizzando il framework è possibile estendere questi rapporti standard o sviluppare rapporti personalizzati completamente nuovi. Il framework di reporting si integra strettamente con i concetti e i principi esistenti di CQ5, in modo che gli sviluppatori possano utilizzare la conoscenza già acquisita di CQ5 come piattaforma di sviluppo per lo sviluppo di rapporti.

Per i rapporti standard forniti con AEM:

* Tali rapporti si basano sul framework di reporting:

   * [Report componente](/help/sites-administering/reporting.md#component-report)
   * [Report attività pagina](/help/sites-administering/reporting.md#page-activity-report)
   * [Report utente](/help/sites-administering/reporting.md#user-report)
   * [Report di istanze flusso di lavoro](/help/sites-administering/reporting.md#workflow-instance-report)

* Le seguenti relazioni si basano su principi individuali e pertanto non possono essere estese:

   * [Utilizzo disco](/help/sites-administering/reporting.md#disk-usage)
   * [Verifica stato](/help/sites-administering/reporting.md#health-check)
   * [Report flusso di lavoro](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>L&#39;esercitazione [Creazione di un report personalizzato - Un esempio](#creating-your-own-report-an-example) mostra anche quanti dei principi riportati di seguito possono essere utilizzati.
>
>Puoi anche fare riferimento ai rapporti standard per vedere altri esempi di implementazione.

>[!NOTE]
>
>Negli esempi e nelle definizioni seguenti è utilizzata la seguente notazione:
>
>* Ogni riga definisce un nodo o una proprietà in cui:
   >
   >  
* `N:<name> [<nodeType>]`
   >
   >     
   Descrive un nodo con il nome di `<*name*>` e il tipo di nodo di `<*nodeType*>`*.*
   >
   >  
* `P:<name> [<propertyType]`
   >
   >     
   Descrive una proprietà con il nome di `<*name*>` e un tipo di proprietà di `<*propertyType*>`.
   >
   >  
* `P:<name> = <value>`
   >
   >     
   Descrive una proprietà `<name>` che deve essere impostata sul valore di `<value>`.
   >
   >
* Il rientro mostra le dipendenze gerarchiche tra i nodi.
>* Elementi separati da | indica un elenco di possibili elementi; ad esempio, tipi o nomi:

>
>  
ad esempio `String|String[]` indica che la proprietà può essere String o String[].
>
>* `[]` rappresenta un array; come [] Stringing o array di nodi come nella definizione [ della ](#query-definition)query.
>
>
Salvo diversa indicazione, i tipi predefiniti sono:
>
>* Nodi - `nt:unstructured`
>* Proprietà - `String`


## Framework di reporting {#reporting-framework}

Il quadro di riferimento per le relazioni si basa sui seguenti principi:

* È interamente basato su set di risultati restituiti da una query eseguita da CQ5 QueryBuilder.
* Il set di risultati definisce i dati visualizzati nel rapporto. Ogni riga del set di risultati corrisponde a una riga nella visualizzazione tabulare del rapporto.
* Le operazioni disponibili per l&#39;esecuzione sul set di risultati sono simili ai concetti RDBMS; principalmente *raggruppamento* e *aggregazione*.

* La maggior parte del recupero e dell&#39;elaborazione dei dati è effettuata sul lato server.
* Il cliente è l&#39;unico responsabile della visualizzazione dei dati preelaborati. Solo le attività di elaborazione secondarie (ad esempio, la creazione di collegamenti nel contenuto di una cella) vengono eseguite sul lato client.

Il framework di reporting (illustrato dalla struttura di un report standard) utilizza i seguenti blocchi predefiniti, alimentati dalla coda di elaborazione:

![chlimage_1-248](assets/chlimage_1-248.png)

### Pagina report {#report-page}

La pagina del rapporto:

* È una pagina standard di CQ5.
* Si basa su un modello [standard CQ5, configurato per il report](#report-template).

### Base report {#report-base}

Il componente [ `reportbase` ](#report-base-component) costituisce la base di qualsiasi rapporto così come è:

* Contiene la definizione della [query](#the-query-and-data-retrieval) che fornisce il set di risultati sottostante di dati.

* È un sistema paragrafo adattato che conterrà tutte le colonne ( `columnbase`) aggiunte al report.
* Definisce i tipi di grafico disponibili e quelli attualmente attivi.
* Definisce la finestra di dialogo Modifica, che consente all’utente di configurare alcuni aspetti del rapporto.

### Base colonna {#column-base}

Ogni colonna è un&#39;istanza del [ `columnbase` componente](#column-base-component) che:

* È un paragrafo, utilizzato da parsys ( `reportbase`) del rispettivo rapporto.
* definisce il collegamento al set di risultati [sottostante](#the-query-and-data-retrieval); ad esempio, definisce i dati specifici a cui si fa riferimento all&#39;interno di questo set di risultati e come viene elaborato.
* contiene definizioni supplementari; quali gli aggregati e i filtri disponibili, insieme a eventuali valori predefiniti.

### Query e recupero dati {#the-query-and-data-retrieval}

Query:

* È definito come parte del componente [ `reportbase`](#report-base).
* Si basa su [CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html).
* Recupera i dati utilizzati come base del rapporto. Ogni riga del set di risultati (tabella) è associata a un nodo come restituito dalla query. Informazioni specifiche per [singole colonne](#column-base-component) vengono quindi estratte da questo set di dati.

* In genere si compone di:

   * Un percorso radice.

      Specifica la struttura ad albero secondaria del repository in cui effettuare la ricerca.

      Per ridurre al minimo l&#39;impatto sulle prestazioni, è consigliabile (provare) limitare la query a un sottoalbero specifico del repository. Il percorso principale può essere predefinito nel [modello di report](#report-template) oppure impostato dall&#39;utente nella finestra di dialogo [Configurazione (Edit)](#configuration-dialog).

   * [Uno o più criteri](#query-definition).

      che sono imposti per produrre l&#39;insieme (iniziale) di risultati; includono, ad esempio, limitazioni relative al tipo di nodo o vincoli di proprietà.

**Il punto chiave qui è che ogni singolo nodo restituito nel set di risultati della query viene utilizzato per generare una singola riga nel report (ovvero una relazione 1:1).**

Lo sviluppatore deve assicurarsi che la query definita per un report restituisca un set di nodi appropriato per quel report. Tuttavia, il nodo stesso non deve contenere tutte le informazioni richieste, ma può anche essere derivato dai nodi padre e/o figlio. Ad esempio, la query utilizzata per il [Rapporto utente](/help/sites-administering/reporting.md#user-report) seleziona i nodi in base al tipo di nodo (in questo caso `rep:user`). Tuttavia, la maggior parte delle colonne del report non prende i propri dati direttamente da questi nodi, ma dai nodi secondari `profile`.

### Coda di elaborazione {#processing-queue}

La [query](#the-query-and-data-retrieval) restituisce un set di risultati di dati da visualizzare come righe nel report. Ogni riga del set di risultati viene elaborata (lato server), in [più fasi](#phases-of-the-processing-queue), prima di essere trasferita al client per la visualizzazione nel report.

Questo consente di:

* Estrazione e derivazione di valori dal set di risultati sottostante.

   Ad esempio, consente di elaborare due valori di proprietà come valore singolo calcolando la differenza tra i due.

* risoluzione dei valori estratti; questo può essere fatto in diversi modi.

   Ad esempio, i percorsi possono essere mappati su un titolo (come nel contenuto leggibile dall&#39;utente della rispettiva proprietà *jcr:title*).

* Applicazione di filtri in diversi punti.
* Se necessario, create dei valori composti.

   Ad esempio, costituito da un testo visualizzato all&#39;utente, un valore da utilizzare per l&#39;ordinamento e un URL aggiuntivo utilizzato (sul lato client) per creare un collegamento.

#### Flusso di lavoro della coda di elaborazione {#workflow-of-the-processing-queue}

Il seguente flusso di lavoro rappresenta la coda di elaborazione:

![chlimage_1-249](assets/chlimage_1-249.png)

#### Fasi della coda di elaborazione {#phases-of-the-processing-queue}

Laddove le fasi e gli elementi dettagliati siano:

1. Trasforma i risultati restituiti dalla [query iniziale (base di report)](#query-definition) nel set di risultati di base utilizzando gli estrattori di valore.

   Gli estrattori di valore vengono scelti automaticamente in base al tipo di colonna [](#column-specific-definitions). Sono utilizzati per leggere i valori dalla query JCR sottostante e creare un set di risultati da essi; dopo di che può essere successivamente applicata un&#39;ulteriore trasformazione. Ad esempio, per il tipo `diff`, l&#39;estrattore di valori legge due proprietà, calcola il valore singolo che viene quindi aggiunto al set di risultati. Impossibile configurare gli estrattori di valore.

1. A tale set di risultati iniziale, contenente dati non elaborati, viene applicato il filtro iniziale [a](#column-specific-definitions) (*fase raw*).

1. I valori sono [preelaborati](#processing-queue); come definito per la fase *apply*.

1. [Il filtraggio](#column-specific-definitions)  (assegnato alla fase  ** preelaborata) viene eseguito sui valori preelaborati.

1. I valori sono risolti; secondo il [risolutore definito](#processing-queue).
1. [Il filtraggio](#column-specific-definitions)  (assegnato alla fase  ** risolta) viene eseguito sui valori risolti.

1. I dati sono [raggruppati e aggregati](#column-specific-definitions).
1. I dati della matrice vengono risolti convertendola in un elenco (basato su stringhe).

   Si tratta di un passaggio implicito che converte un risultato con più valori in un elenco che può essere visualizzato; è richiesto per i valori delle celle (non aggregati) basati su proprietà JCR con più valori.

1. I valori sono di nuovo [preelaborati](#processing-queue); come definito per la fase *afterApply*.

1. I dati sono ordinati.
1. I dati elaborati vengono trasferiti al client.

>[!NOTE]
>
>La query iniziale che restituisce il set di risultati dei dati di base è definita per il componente `reportbase`.
>
>Altri elementi della coda di elaborazione sono definiti sui componenti `columnbase`.

## Costruzione report e configurazione {#report-construction-and-configuration}

Per creare e configurare un rapporto sono necessari i seguenti elementi:

* una [posizione per la definizione dei componenti del report](#location-of-report-components)
* a [ `reportbase` componente](#report-base-component)
* uno o più componenti [ `columnbase`](#column-base-component)
* a [componente pagina](#page-component)
* a [report design](#report-design)
* a [modello di report](#report-template)

### Posizione dei componenti del report {#location-of-report-components}

I componenti di reporting predefiniti sono contenuti in `/libs/cq/reporting/components`.

Tuttavia, si consiglia vivamente di non aggiornare tali nodi, ma di creare nodi componenti personalizzati in `/apps/cq/reporting/components` o se appropriato `/apps/<yourProject>/reports/components`.

Dove (ad esempio):

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

In questo modo si crea il livello principale per il rapporto e sotto di esso, il componente base del rapporto e i componenti di base delle colonne:

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### Componente pagina {#page-component}

Una pagina di report deve utilizzare il simbolo `sling:resourceType` di `/libs/cq/reporting/components/reportpage`.

Nella maggior parte dei casi, non deve essere necessario personalizzare un componente pagina.

## Componente base report {#report-base-component}

Ogni tipo di rapporto richiede un componente contenitore derivato da `/libs/cq/reporting/components/reportbase`.

Questo componente funge da contenitore per il rapporto nel suo insieme e fornisce informazioni per:

* La [definizione query](#query-definition).
* Una finestra di dialogo [(opzionale)](#configuration-dialog) per la configurazione del rapporto.
* Qualsiasi [Charts](#chart-definitions) integrato nel rapporto.

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### Definizione query {#query-definition}

```xml
N:queryBuilder
    N:propertyConstraints
    [
        N:<name> // array of nodes (name irrelevant), each with the following properties:
            P:name
            P:value
    ]
    P:nodeTypes [String|String[]]
    P:mandatoryProperties [String|String[]
  ]
```

* `propertyConstraints`

   Può essere utilizzato per limitare il set di risultati a nodi con proprietà specifiche con valori specifici. Se vengono specificati più vincoli, il nodo deve soddisfare tutti questi vincoli (operazione AND).

   Esempio:

   ```
   N:propertyConstraints
    [
    N:0
    P:sling:resourceType
    P:foundation/components/textimage
    N:1
    P:jcr:modifiedBy
    P:admin
    ]
   ```

   Restituirebbe tutti i componenti `textimage` modificati per l&#39;ultima volta dall&#39;utente `admin`.

* `nodeTypes`

   Utilizzato per limitare il set di risultati ai tipi di nodo specificati. È possibile specificare più tipi di nodi.

* `mandatoryProperties`

   Può essere utilizzato per limitare il set di risultati ai nodi con *all* delle proprietà specificate. Il valore delle proprietà non viene preso in considerazione.

Tutte le opzioni sono facoltative e possono essere combinate come necessario, ma è necessario definirne almeno una.

### Definizioni grafico {#chart-definitions}

```xml
N:charting
    N:settings
        N:active [cq:WidgetCollection]
        [
            N:<name> // array of nodes, each with the following property
                P:id   // must match the id of a child node of definitions
        ]
    N:definitions [cq:WidgetCollection]
    [
        N:<name> // array of nodes, each with the following properties
            P:id
            P:type
            // additional, chart type specific configurations
    ]
```

* `settings`

   Contiene le definizioni per i grafici attivi.

   * `active`

      Poiché è possibile definire più impostazioni, è possibile utilizzarle per definire quali sono attualmente attive. Questi sono definiti da una serie di nodi (non esiste una convenzione di denominazione obbligatoria per questi nodi, ma i report standard spesso utilizzano `0`, `1`. `x`), ciascuna con la seguente proprietà:

      * `id`

         Identificazione dei grafici attivi. Deve corrispondere all&#39;ID di uno dei grafici `definitions`.

* `definitions`

   Definisce i tipi di grafico potenzialmente disponibili per il rapporto. Le `definitions` da utilizzare verranno specificate dalle impostazioni `active`.

   Le definizioni vengono specificate utilizzando un array di nodi (spesso denominati `0`, `1`. `x`), ciascuna con le seguenti proprietà:

   * `id`

      Identificazione del grafico.

   * `type`

      Tipo di grafico disponibile. Seleziona da:

      * `pie`
Grafico a torta. Generato solo dai dati correnti.

      * `lineseries`
Serie di linee (punti di connessione che rappresentano le istantanee effettive). Generato solo dai dati storici.
   * A seconda del tipo di grafico sono disponibili ulteriori proprietà:

      * per il tipo di grafico `pie`:

         * `maxRadius` ( `Double/Long`)

            Raggio massimo consentito per il grafico a torta; pertanto la dimensione massima consentita per il grafico (senza legenda). Ignorato se è definito `fixedRadius`.

         * `minRadius` ( `Double/Long`)

            Raggio minimo consentito per il grafico a torta. Ignorato se è definito `fixedRadius`.

         * `fixedRadius` (  `Double/Long`) Definisce un raggio fisso per il grafico a torta.
      * per il tipo di grafico [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

            True se deve essere visualizzata una riga aggiuntiva che mostra il **Totale**.
impostazione predefinita: `false`

         * `series` ( `Long`)

            Numero di righe/serie da visualizzare.
default: `9` (è anche il massimo consentito)

         * `hoverLimit` ( `Long`)

            Numero massimo di istantanee aggregate (punti visualizzati su ogni linea orizzontale, che rappresentano valori distinti) per le quali devono essere visualizzati i pop-up, ossia quando l&#39;utente passa il puntatore del mouse su un valore distinto o un&#39;etichetta corrispondente nella legenda del grafico.

            default: `35` (ossia, se per le impostazioni correnti del grafico non sono disponibili più di 35 valori distinti, non vengono visualizzati alcun risultato).

            Esiste un ulteriore limite di 10 popup che possono essere mostrati in parallelo (più popup possono essere mostrati quando il mouse sopra i testi della legenda).



### Finestra di dialogo Configurazione {#configuration-dialog}

Ogni rapporto può avere una finestra di dialogo di configurazione, che consente all&#39;utente di specificare vari parametri per il rapporto. Questa finestra di dialogo è accessibile tramite il pulsante **Modifica** all&#39;apertura della pagina del rapporto.

Questa finestra di dialogo è una [finestra](/help/sites-developing/components-basics.md#dialogs) standard di CQ e può essere configurata come tale (per ulteriori informazioni, vedere [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) ).

Esempio di finestra di dialogo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Dialog"
    height="{Long}424">
    <items jcr:primaryType="cq:WidgetCollection">
        <props jcr:primaryType="cq:Panel">
            <items jcr:primaryType="cq:WidgetCollection">
                <title
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/title.infinity.json"
                    xtype="cqinclude"/>
                <description
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/description.infinity.json"
                    xtype="cqinclude"/>
                <rootPath
                    jcr:primaryType="cq:Widget"
                    fieldLabel="Root path"
                    name="./report/rootPath"
                    rootPath=""
                    rootTitle="Repository root"
                    xtype="pathfield"/>
                <processing
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/processing.infinity.json"
                    xtype="cqinclude"/>
                <scheduling
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/scheduling.infinity.json"
                    xtype="cqinclude"/>
            </items>
        </props>
    </items>
</jcr:root>
```

Sono disponibili diversi componenti preconfigurati; è possibile fare riferimento a questi elementi nella finestra di dialogo utilizzando la proprietà `xtype` con un valore di `cqinclude`:

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   Campo di testo per definire il titolo del rapporto.

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   Area di testo per definire la descrizione del rapporto.

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   Selettore per la modalità di elaborazione del rapporto (caricamento manuale o automatico dei dati).

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   Selettore per la pianificazione di istantanee per il grafico storico.

>[!NOTE]
>
>I componenti di riferimento devono essere inclusi utilizzando il suffisso `.infinity.json` (vedere l&#39;esempio precedente).

### Percorso directory principale {#root-path}

È inoltre possibile definire un percorso radice per il report:

* **`rootPath`**

   Questo limita il rapporto a una determinata sezione (struttura ad albero o sottostruttura) del repository, consigliata per l&#39;ottimizzazione delle prestazioni. Il percorso principale è specificato dalla proprietà `rootPath` del nodo `report` di ciascuna pagina di report (ripresa dal modello al momento della creazione della pagina).

   Può essere specificato da:

   * il [modello di report](#report-template) (come valore fisso o come valore predefinito per la finestra di dialogo di configurazione).
   * l&#39;utente (utilizzando questo parametro)

## Componente base colonna {#column-base-component}

Ogni tipo di colonna richiede un componente derivato da `/libs/cq/reporting/components/columnbase`.

Un componente per colonna definisce una combinazione di quanto segue:

* La configurazione [Query specifica per la colonna](#column-specific-query).
* [Risolutori e pre-elaborazione](#resolvers-and-preprocessing).
* Le [Definizioni specifiche della colonna](#column-specific-definitions) (ad esempio filtri e aggregati); `definitions` nodo figlio).
* [Valori](#column-default-values) predefiniti colonna.
* Il [Filtro client](#client-filter) per estrarre le informazioni da visualizzare dai dati restituiti dal server.
* Inoltre, un componente colonna deve fornire un&#39;istanza appropriata di `cq:editConfig`. per definire gli [Eventi e azioni](#events-and-actions) richiesti.
* Configurazione per [colonne generiche](#generic-columns).

```
N:<columnname> [cq:Component]
    P:componentGroup
    P:jcr:title
    P:sling:resourceSuperType = "cq/reporting/components/columnbase"
    N:cq:editConfig [cq:EditConfig] // <a href="#events-and-actions">Events and Actions</a>
    N:defaults // <a href="#column-default-values">Column Default Values</a>
    N:definitions
      N:queryBuilder // <a href="#column-specific-query">Column Specific Query</a>
        P:property [String|String[]] // Column Specific Query
        P:subPath // Column Specific Query
        P:secondaryProperty [String|String[]] // Column Specific Query
        P:secondarySubPath // Column Specific Query
      N:data
        P:clientFilter [String] // <a href="#client-filter">Client Filter</a>
        P:resolver // <a href="#resolvers-and-preprocessing">Resolvers and Preprocessing</a>
        N:resolverConfig // Resolvers and Preprocessing
        N:preprocessing // Resolvers and Preprocessing
      P:type // <a href="#column-specific-definitions">Column Specific Definitions</a>
      P:groupable [Boolean] // Column Specific Definitions
      N:filters [cq:WidgetCollection] // Column Specific Definitions
      N:aggregates [cq:WidgetCollection] // Column Specific Definitions
```

Vedere anche [Definizione del nuovo report](#defining-your-new-report).

### Query specifica colonna {#column-specific-query}

Definisce l&#39;estrazione dati specifica (dal [set di risultati dei dati del report](#the-query-and-data-retrieval)) da utilizzare nella singola colonna.

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

   Definisce la proprietà da utilizzare per calcolare il valore effettivo della cella.

   Se la proprietà è definita come String[], vengono scansionate più proprietà (in sequenza) per trovare il valore effettivo.

   Ad esempio, nel caso di:

   `property = [ "jcr:lastModified", "jcr:created" ]`

   L&#39;estrattore di valore corrispondente (qui sotto il comando):

   * Verificate che sia disponibile una proprietà jcr:lastModified e, in tal caso, utilizzatela.
   * Se non è disponibile alcuna proprietà jcr:lastModified, verrà utilizzato il contenuto di jcr:created.

* `subPath`

   Se il risultato non si trova sul nodo restituito dalla query, `subPath` definisce la posizione effettiva della proprietà.

* `secondaryProperty`

   definisce una seconda proprietà che deve essere utilizzata anche per calcolare il valore effettivo della cella; questo verrà utilizzato solo per alcuni tipi di colonna (diff e sortable).

   Ad esempio, nel caso del report Istanze flusso di lavoro, la proprietà specificata viene utilizzata per memorizzare il valore effettivo della differenza di tempo (in millisecondi) tra l&#39;ora iniziale e quella finale.

* `secondarySubPath`

   Simile a subPath, quando si utilizza `secondaryProperty`.

Nella maggior parte dei casi, verrà utilizzato solo `property`.

### Filtro client {#client-filter}

Il filtro client estrae le informazioni da visualizzare dai dati restituiti dal server.

>[!NOTE]
>
>Questo filtro viene eseguito sul lato client, dopo che è stata applicata l&#39;intera elaborazione sul lato server.

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` è definita come funzione JavaScript che:

* come input, riceve un parametro; i dati restituiti dal server (così preelaborati)
* come output, restituisce il valore filtrato (elaborato); i dati estratti o derivati dalle informazioni di input

L’esempio seguente estrae il percorso di pagina corrispondente da un percorso di componente:

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### Risolutori e pre-elaborazione {#resolvers-and-preprocessing}

La [coda di elaborazione](#processing-queue) definisce i vari risolutori e configura la preelaborazione:

```xml
N:definitions
    N:data
        P:resolver
        N:resolverConfig
        N:preprocessing
            N:apply
            N:applyAfter
```

* `resolver`

   Definisce il risolutore da utilizzare. Sono disponibili i seguenti risolutori:

   * `const`

      Mappa i valori ad altri valori; ad esempio, viene utilizzato per risolvere costanti come `en` con il valore equivalente `English`.

   * `default`

      Il risolutore predefinito. Questo è un risolutore fittizio che in realtà non risolve nulla.

   * `page`

      risolve un valore di percorso al percorso della pagina appropriata; più precisamente, al nodo `jcr:content` corrispondente. Ad esempio, `/content/.../page/jcr:content/par/xyz` è risolto in `/content/.../page/jcr:content`.

   * `path`

      Risolve un valore di percorso aggiungendo facoltativamente un percorso secondario e prendendo il valore effettivo da una proprietà del nodo (come definito da `resolverConfig`) nel percorso risolto. Ad esempio, è possibile risolvere un `path` di `/content/.../page/jcr:content` nel contenuto della proprietà `jcr:title`, il che significa che il percorso di pagina viene risolto nel titolo della pagina.

   * `pathextension`

      Risolve un valore anteponendo un percorso e prendendo il valore effettivo da una proprietà del nodo nel percorso risolto. Ad esempio, un valore `de` potrebbe essere preceduto da un percorso come `/libs/wcm/core/resources/languages`, che sfrutta il valore della proprietà `language`, per risolvere il codice del paese `de` nella descrizione della lingua `German`.

* `resolverConfig`

   Fornisce le definizioni per il risolutore; le opzioni disponibili dipendono dalla `resolver` selezionata:

   * `const`

      Utilizzare le proprietà per specificare le costanti per la risoluzione. Il nome della proprietà definisce la costante da risolvere; il valore della proprietà definisce il valore risolto.

      Ad esempio, una proprietà con **Name**= `1` e **Value** `=One` risolverà 1 in Uno.

   * `default`

      Nessuna configurazione disponibile.

   * `page`

      * `propertyName` (facoltativo)

         Definisce il nome della proprietà da utilizzare per risolvere il valore. Se non viene specificato, viene utilizzato il valore predefinito *jcr:title* (il titolo della pagina); per il risolutore `page`, questo significa che prima il percorso viene risolto nel percorso della pagina, quindi ulteriormente risolto nel titolo della pagina.
   * `path`

      * `propertyName` (facoltativo)

         Specifica il nome della proprietà da utilizzare per risolvere il valore. Se non viene specificato, viene utilizzato il valore predefinito `jcr:title`.

      * `subPath` (facoltativo)

         Questa proprietà può essere utilizzata per specificare un suffisso da aggiungere al percorso prima della risoluzione del valore.
   * `pathextension`

      * `path` (mandatory)

         Definisce il percorso da anteporre.

      * `propertyName` (obbligatorio)

         Definisce la proprietà sul percorso risolto in cui si trova il valore effettivo.

      * `i18n` (facoltativo; type Boolean)

         Determina se il valore risolto deve essere *internazionalizzato* (ovvero mediante i servizi di internazionalizzazione di [CQ5](/help/sites-administering/tc-manage.md)).



* `preprocessing`

   La preelaborazione è facoltativa e può essere associata (separatamente) alle fasi di elaborazione *applicare* o *applicareAfter*:

   * `apply`

      Fase di preelaborazione iniziale ([passaggio 3 nella rappresentazione della coda di elaborazione](#processing-queue)).

   * `applyAfter`

      Applicare dopo la preelaborazione ([passaggio 9 nella rappresentazione della coda di elaborazione](#processing-queue)).

#### Risolutori {#resolvers}

I risolutori vengono utilizzati per estrarre le informazioni richieste. Alcuni esempi dei vari risolutori sono:

**Contenuti**

Di seguito viene risolto un valore costante di `VersionCreated` nella stringa `New version created`.

Consulta `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**Pagina**

Risolve un valore di percorso alla proprietà jcr:description sul nodo jcr:content (figlio) della pagina corrispondente.

Consulta `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**Percorso**

Quanto segue risolve un percorso di `/content/.../page` al contenuto della proprietà `jcr:title`, il che significa che il percorso di pagina viene risolto nel titolo della pagina.

Consulta `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**Estensione percorso**

Il valore seguente viene anteposto a `de` con l&#39;estensione percorso `/libs/wcm/core/resources/languages`, quindi prende il valore dalla proprietà `language`, per risolvere il codice del paese `de` alla descrizione della lingua `German`.

Consulta `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### Pre-elaborazione {#preprocessing}

La definizione `preprocessing` può essere applicata a:

* valore originale:

   La definizione di preelaborazione per il valore originale viene specificata direttamente in `apply` e/o `applyAfter`.

* nel suo stato aggregato:

   Se necessario, è possibile fornire una definizione separata per ogni aggregazione.

   Per specificare la preelaborazione esplicita per i valori aggregati, le definizioni di preelaborazione devono risiedere in un rispettivo nodo secondario `aggregated` ( `apply/aggregated`, `applyAfter/aggregated`). Se è richiesta la preelaborazione esplicita per gli aggregati distinti, la definizione di preelaborazione si trova su un nodo secondario con il nome del rispettivo aggregato (ad esempio `apply/aggregated/min/max` o altri aggregati).

Durante la preelaborazione potete specificare una delle seguenti opzioni:

* [trova e sostituisce ](#preprocessing-find-and-replace-patterns)
i patternQuando viene trovato, il pattern specificato (definito come espressione regolare) viene sostituito da un altro pattern; ad esempio, può essere utilizzato per estrarre una sottostringa dell&#39;originale.

* [formattatori del tipo di dati](#preprocessing-data-type-formatters)

   Converte un valore numerico in una stringa relativa; ad esempio, il valore &quot;che rappresenta una differenza di ora di 1 ora&quot; viene risolto in una stringa come `1:24PM (1 hour ago)`.

Esempio:

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply|applyAfter
                P:pattern         // regex
                P:replace         // replacement for regex
                // and/or
                P:format          // data type formatter
```

#### Pre-elaborazione - Trova e sostituisci pattern {#preprocessing-find-and-replace-patterns}

Per la preelaborazione è possibile specificare un `pattern` (definito come [espressione regolare](https://en.wikipedia.org/wiki/Regular_expression) o regex) che si trova e quindi sostituito dal pattern `replace`:

* `pattern`

   Espressione regolare utilizzata per individuare una sottostringa.

* `replace`

   Stringa o rappresentazione della stringa che verrà utilizzata come sostituzione della stringa originale. Spesso questo rappresenta una sottostringa della stringa ubicata dall&#39;espressione regolare `pattern`.

Un esempio di sostituzione può essere suddiviso come:

* Per il nodo `definitions/data/preprocessing/apply` con le due seguenti proprietà:

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`:  `$1`

* Stringa in arrivo come:

   * `/content/geometrixx/en/services/jcr:content/par/text`

* Saranno suddivise in quattro sezioni:

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` -  `(/jcr:content)` -  `/jcr:content`
   * `$3` -  `(/|$)` -  `/`
   * `$4` -  `(.*)` -  `par/text`

* E sostituito con la stringa rappresentata da `$1`:

   * `/content/geometrixx/en/services`

#### Pre-elaborazione - Tipo di dati per materie {#preprocessing-data-type-formatters}

Questi formati convertono un valore numerico in una stringa relativa.

Ad esempio, questo può essere utilizzato per una colonna temporale che consente gli aggregati `min`, `avg` e `max`. Gli aggregati `min`/ `avg`/ `max` vengono visualizzati come *differenza di tempo* (ad esempio `10 days ago`), richiedono un formattatore di dati. A questo scopo, un formattatore `datedelta` viene applicato ai valori aggregati `min`/ `avg`/ `max`. Se è disponibile anche un&#39;aggregazione `count`, non è necessario aggiungere un formattatore, né il valore originale.

Attualmente i formati dei tipi di dati disponibili sono:

* `format`

   Formattatore tipo dati:

   * `duration`

      La durata è l&#39;intervallo di tempo tra due date definite. Ad esempio, l’inizio e la fine di un’azione del flusso di lavoro che richiedeva 1 ora, a partire dalle 13/13/11 11:23 e fino a un’ora dopo alle 13/13/11 12:23.

      Converte un valore numerico (interpretato come millisecondi) in una stringa di durata; ad esempio, `30000` è formattato come * `30s`.*

   * `datedelta`

      Datadelta è l&#39;intervallo di tempo tra una data passata e quella &quot;ora&quot; (quindi avrà un risultato diverso se il rapporto viene visualizzato in un momento successivo).

      Converte il valore numerico (interpretato come differenza di ora in giorni) in una stringa data relativa. Ad esempio, 1 è formattato come 1 giorno fa.

L&#39;esempio seguente definisce la formattazione `datedelta` per gli aggregati `min` e `max`:

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply
                N:aggregated
                    N:min
                        P:format = "datedelta"
                    N:max
                        P:format = "datedelta"
```

### Definizioni specifiche delle colonne {#column-specific-definitions}

Le definizioni specifiche della colonna definiscono i filtri e gli aggregati disponibili per quella colonna.

```xml
N:definitions
    P:type
    P:groupable [Boolean]
    N:filters [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:filterType
            P:id
            P:phase
    ]
    N:aggregates [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:text
            P:type
    ]
```

* `type`

   Sono disponibili le seguenti opzioni standard:

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

      Viene utilizzato per estrarre parti di una data necessarie per l&#39;aggregazione (ad esempio, gruppi per anno per ottenere i dati aggregati per ogni anno).

   * `sortable`

      Viene utilizzato per i valori che utilizzano valori diversi (ricavati da proprietà diverse) per l&#39;ordinamento e la visualizzazione.
   Inoltre. uno dei valori di cui sopra può essere definito come valore multiplo; ad esempio, `string[]` definisce un array di stringhe.

   L&#39;estrattore di valori viene scelto in base al tipo di colonna. Se per un tipo di colonna è disponibile un estrattore di valori, viene utilizzato questo estrattore. In caso contrario, viene utilizzato l&#39;estrattore di valore predefinito.

   Un tipo può (facoltativamente) accettare un parametro. Ad esempio, `timeslot:year` estrae l&#39;anno da un campo data. Tipi con i relativi parametri:

   * `timeslot` - I valori sono paragonabili alle costanti corrispondenti di  `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` -  `Calendar.MONTH`
      * `timeslot:week-of-year` -  `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` -  `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` -  `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` -  `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` -  `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` -  `Calendar.MINUTE`


* `groupable`

   Definisce se il rapporto può essere raggruppato per questa colonna.

* `filters`

   Definizioni dei filtri.

   * `filterType`

      I filtri disponibili sono:

      * `string`

         Un filtro basato su stringa.
   * `id`

      Identificatore filtro.

   * `phase`

      Fasi disponibili:

      * `raw`

         Il filtro viene applicato ai dati non elaborati.

      * `preprocessed`

         Il filtro viene applicato ai dati preelaborati.

      * `resolved`

         Il filtro viene applicato ai dati risolti.


* `aggregates`

   Aggrega definizioni.

   * `text`

      Nome testuale dell&#39;aggregazione. Se `text` non è specificato, verrà utilizzata la descrizione predefinita dell&#39;aggregazione; ad esempio, `minimum` verrà utilizzato per l&#39;aggregazione `min`.

   * `type`

      Tipo di aggregazione. Gli aggregati disponibili sono:

      * `count`

         Conta il numero di righe.

      * `count-nonempty`

         Conta il numero di righe non vuote.

      * `min`

         Fornisce il valore minimo.

      * `max`

         Fornisce il valore massimo.

      * `average`

         Fornisce il valore medio.

      * `sum`

         Fornisce la somma di tutti i valori.

      * `median`

         Fornisce il valore medio.

      * `percentile95`

         Prende il 95° percentile di tutti i valori.

### Valori predefiniti colonna {#column-default-values}

Viene utilizzato per definire i valori predefiniti per la colonna:

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   I valori `aggregate` validi sono gli stessi di `type` in `aggregates` (vedere [Definizioni specifiche per le colonne (definizioni - filtri / aggregati)](#column-specific-definitions) ).

### Eventi e azioni {#events-and-actions}

Edit Configuration (Modifica configurazione) definisce gli eventi necessari ai listener per rilevare e le azioni da applicare dopo che si sono verificati tali eventi. Per informazioni di base, vedere [introduzione allo sviluppo di componenti](/help/sites-developing/components.md).

È necessario definire i seguenti valori per garantire che tutte le azioni richieste siano soddisfatte:

```xml
N:cq:editConfig [cq:EditConfig]
    P:cq:actions [String[]] = "insert", "delete"
    P:cq:dialogMode = "floating"
    P:cq:layout = "auto"
    N:cq:listeners [cq:EditListenersConfig]
        P:aftercreate = "REFRESH_INSERTED"
        P:afterdelete = "REFRESH_SELF"
        P:afteredit = "REFRESH_SELF"
        P:afterinsert = "REFRESH_INSERTED"
        P:aftermove = "REFRESH_SELF"
        P:afterremove = "REFRESH_SELF"
```

### Colonne generiche {#generic-columns}

Le colonne generiche sono un&#39;estensione in cui (la maggior parte) le definizioni di colonna sono memorizzate nell&#39;istanza del nodo di colonna (anziché nel nodo del componente).

Usano una finestra di dialogo (standard), che potete personalizzare, per il singolo componente generico. Questa finestra di dialogo consente all&#39;utente del report di definire le proprietà delle colonne di una colonna generica nella pagina del report (utilizzando l&#39;opzione di menu **Proprietà delle colonne...**).

Un esempio è rappresentato dalla colonna **Generico** del report utente **Report utente**; vedere `/libs/cq/reporting/components/userreport/genericcol`.

Per creare una colonna generica:

* Impostare la proprietà `type` del nodo `definition` della colonna su `generic`.

   Consulta `/libs/cq/reporting/components/userreport/genericcol/definitions`

* Specificate una definizione di finestra di dialogo (standard) sotto il nodo `definition` della colonna.

   Consulta `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * I campi della finestra di dialogo devono fare riferimento agli stessi nomi della proprietà del componente corrispondente (incluso il percorso).

      Ad esempio, se si desidera rendere configurabile il tipo di colonna generica tramite la finestra di dialogo, utilizzare un campo con il nome `./definitions/type`.

   * Le proprietà definite mediante l&#39;interfaccia utente/finestra di dialogo hanno la precedenza su quelle definite nel componente `columnbase`.

* Definite Edit Configuration (Modifica configurazione).

   Consulta `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* Utilizzare metodologie AEM standard per definire (ulteriori) proprietà delle colonne.

   Tenere presente che per le proprietà definite nelle istanze di componenti e colonne, il valore nell’istanza di colonna ha la precedenza.

   Le proprietà disponibili per una colonna generica sono:

   * `jcr:title` - nome colonna
   * `definitions/aggregates` - aggregati
   * `definitions/filters` - filtri
   * `definitions/type`- il tipo di colonna (deve essere definito nella finestra di dialogo, utilizzando un selettore/una casella di controllo o un campo nascosto)
   * `definitions/data/resolver` e  `definitions/data/resolverConfig` (ma non  `definitions/data/preprocessing` o  `.../clientFilter`) - il risolutore e la configurazione
   * `definitions/queryBuilder` - la configurazione del generatore di query
   * `defaults/aggregate` - l&#39;aggregato predefinito

   Nel caso di una nuova istanza della colonna generica nel **Rapporto utente**, le proprietà definite con la finestra di dialogo sono persistenti in:

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## Struttura report {#report-design}

La struttura definisce i tipi di colonna disponibili per la creazione di un rapporto. Definisce inoltre il sistema paragrafo a cui vengono aggiunte le colonne.

Si consiglia vivamente di creare una singola progettazione per ciascun rapporto. Ciò garantisce la massima flessibilità. Vedere anche [Definizione del nuovo report](#defining-your-new-report).

I componenti di reporting predefiniti sono contenuti in `/etc/designs/reports`.

La posizione dei rapporti può dipendere dalla posizione in cui si trovano i componenti:

* `/etc/designs/reports/<yourReport>` è adatto se il rapporto è situato sotto  `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` per i report che utilizzano il  `/apps/<yourProject>/reports` pattern

Le proprietà di progettazione necessarie sono registrate in `jcr:content/reportpage/report/columns` (ad esempio, `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

   Qualsiasi componente e/o gruppo di componenti consentiti nel rapporto.

* `sling:resourceType`

   Proprietà con valore `cq/reporting/components/repparsys`.

Un frammento di progettazione di esempio (tratto dalla progettazione del rapporto sul componente) è:

```xml
<!-- ... -->
    <jcr:content
        jcr:primaryType="nt:unstructured"
        jcr:title="Component Report"
        sling:resourceType="wcm/core/components/designer">
        <reportpage jcr:primaryType="nt:unstructured">
            <report jcr:primaryType="nt:unstructured">
                <columns
                    jcr:primaryType="nt:unstructured"
                    sling:resourceType="cq/reporting/components/repparsys"
                    components="group:Component Report"/>
            </report>
        </reportpage>
    </jcr:content>
<!-- ... -->
```

Non è necessario specificare le strutture per singole colonne. Le colonne disponibili possono essere definite in modalità di progettazione.

>[!NOTE]
>
>È consigliabile non apportare modifiche alle strutture dei rapporti standard. In questo modo si evita di perdere eventuali modifiche durante l&#39;aggiornamento o l&#39;installazione degli hotfix.
>
>Per personalizzare un rapporto standard, copiate il rapporto e la relativa progettazione.

>[!NOTE]
>
>Le colonne predefinite possono essere create automaticamente quando viene creato un rapporto. Questi sono specificati nel modello.

## Modello report {#report-template}

Ogni tipo di rapporto deve fornire un modello. Sono modelli [CQ](/help/sites-developing/templates.md) standard e possono essere configurati come tali.

Il modello deve:

* impostare `sling:resourceType` su `cq/reporting/components/reportpage`

* indicare la progettazione da utilizzare
* creare un nodo secondario `report` che faccia riferimento al componente contenitore ( `reportbase`) tramite la proprietà `sling:resourceType`

Un frammento di modello di esempio (tratto dal modello di rapporto dei componenti) è:

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/compreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

Un frammento di modello di esempio, che mostra la definizione del percorso principale (tratto dal modello di rapporto utente), è:

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/userreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            rootPath="/home/users"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

I modelli di reporting predefiniti sono contenuti in `/libs/cq/reporting/templates`.

Tuttavia, si consiglia vivamente di non aggiornare tali nodi, ma di creare nodi componenti personalizzati in `/apps/cq/reporting/templates` o se appropriato `/apps/<yourProject>/reports/templates`.

Dove, ad esempio (vedere anche [Posizione dei componenti del report](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

In questa sezione viene creata la directory principale per il modello:

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## Creazione di un report personalizzato - Esempio {#creating-your-own-report-an-example}

### Definizione del nuovo report {#defining-your-new-report}

Per definire un nuovo rapporto è necessario creare e configurare:

1. Radice per i componenti del report.
1. Il componente base del report.
1. Uno o più componenti a base di colonna.
1. La struttura del report.
1. Livello principale per il modello di rapporto.
1. Modello di rapporto.

Per illustrare questi passaggi, l&#39;esempio seguente definisce un rapporto in cui sono elencate tutte le configurazioni OSGi all&#39;interno del repository; ovvero tutte le istanze del nodo `sling:OsgiConfig`.

>[!NOTE]
>
>Copiare un rapporto esistente e quindi personalizzare la nuova versione è un metodo alternativo.

1. Crea il nodo principale per il nuovo report.

   Ad esempio, in `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. Definite la base di report. Ad esempio `osgireport[cq:Component]` in `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:osgireport [cq:Component]
           P:sling:resourceSuperType [String] = "cq/reporting/components/reportbase"
           N:charting [nt:unstructured]
               N:settings [nt:unstructured]
                   N:active [cq:WidgetCollection]
                       N:0 [nt:unstructured]
                           P:id [String] = "pie"
                       N:1 [nt:unstructured]
                           P:id [String] = "lineseries"
               N:definitions [cq:WidgetCollections]
                   N:0 [nt:unstructured]
                       P:id [String] = "pie"
                       P:maxRadius [Long] = 180
                       P:type [String] = "pie"
                   N:1 [nt:unstructured]
                       P:id [String] = "lineseries"
                       P:type [String] = "lineseries"
           N:dialog [cq:Dialog]
               P:height [Long] = 424
               N:items [cq:WidgetCollection]
                   N:props [cq:Panel]
                       N:items [cq:WidgetCollection]
                           N:title [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/title.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:description [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/description.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:rootPath [cq:Widget]
                               P:fieldLabel [String] = "Root path"
                               P:name [String] = "./report/rootPath"
                               P:xtype [String] = "pathfield"
                           N:processing [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/processing.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:scheduling [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/scheduling.infinity.json"
                               P:xtype [String] = "cqinclude"
           N:queryBuilder [nt:unstructured]
               P:nodeTypes [String[]] = "sling:OsgiConfig"
   ```

   Definisce un componente base di report che:

   * cerca tutti i nodi di tipo `sling:OsgiConfig`
   * visualizza i grafici `pie` e `lineseries`
   * fornisce una finestra di dialogo che consente all&#39;utente di configurare il rapporto

1. Definire il primo componente di colonna (columnbase). Ad esempio `bundlecol[cq:Component]` in `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:bundlecol [cq:Component]
           P:componentGroup [String] = "OSGi Report"
           P:jcr:title = "Bundle"
           P:sling:resourceSuperType [String] = "cq/reporting/components/columnbase"
           N:cq:editConfig [cq:EditConfig]
               P:cq:actions [String[]] = "insert", "delete"
               P:cq:dialogMode [String] = "floating"
               P:cq:layout [String] = "auto"
               N:cq:listeners [cq:EditListenersConfig]
                   P:aftercreate [String] "REFRESH_INSERTED"
                   P:afterdelete [String] "REFRESH_SELF"
                   P:afteredit [String] "REFRESH_SELF"
                   P:afterinsert [String] "REFRESH_INSERTED"
                   P:aftermove [String] "REFRESH_SELF"
                   P:afterremove [String] "REFRESH_SELF"
           N:defaults [nt:unstructured]
               P:aggregate [String] = "count"
           N:definitions [nt:unstructured]
               P:groupable [Boolean] = false
               P:type [String] = "string"
               N:queryBuilder [nt:unstructured]
                   P:property [String] = "jcr:path"
   ```

   Definisce un componente base di colonna che:

   * cerca e restituisce il valore ricevuto dal server; in questo caso, la proprietà `jcr:path` per ogni nodo `sling:OsgiConfig`
   * fornisce l&#39;aggregazione `count`
   * non raggruppabile
   * ha il titolo `Bundle` (titolo colonna all&#39;interno della tabella)
   * si trova nel gruppo della barra laterale `OSGi Report`
   * aggiorna in corrispondenza di eventi specificati

   >[!NOTE]
   >
   >In questo esempio non esistono definizioni di `N:data` e `P:clientFilter`. Questo perché il valore ricevuto dal server viene restituito su base 1:1, che è il comportamento predefinito.
   >
   >Si tratta delle stesse definizioni:
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >Se la funzione restituisce semplicemente il valore ricevuto.

1. Definite la struttura del rapporto. Ad esempio `osgireport[cq:Page]` in `/etc/designs/reports`.

   ```xml
   N:osgireport [cq:Page]
       N:jcr:content [nt:unstructured]
           P:jcr:title [String] = "OSGi report"
           P:sling:resourceType [String] = "wcm/core/components/designer"
           N:reportpage [nt:unstructured]
               N:report [nt:unstructured]
                   N:columns [nt:unstructured]
                       P:components [String] = "group:OSGi Report"
                       P:sling:resourceType [String] = "cq/reporting/components/repparsys"
   ```

1. Crea il nodo principale per il nuovo modello di rapporto.

   Ad esempio, in `/apps/cq/reporting/templates/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. Definite il modello di rapporto. Ad esempio `osgireport[cq:Template]` in `/apps/cq/reporting/templates`.

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create a new OSGi report."
       P:jcr:title [String] = "OSGi Report Template"
       P:ranking [Long] = 100
       P:shortTitle [String] = "OSGi Report"
       N:jcr:content [cq:PageContent]
           P:cq:designPath [String] = "/etc/designs/reports/osgireport"
           P:sling:resourceType [String] = "cq/reporting/components/reportpage"
           N:report [nt:unstructured]
               P:rootPath [String] = "/"
               P:sling:resourceType [String] = "cq/reporting/components/osgireport/osgireport"
       N:thumbnail.png [nt:file]
   ```

   Definisce un modello che:

   * definisce la `allowedPaths` per i report risultanti, nel caso precedente in un punto qualsiasi all&#39;interno di `/etc/reports`
   * fornisce titoli e descrizioni per il modello
   * fornisce un&#39;immagine in miniatura da utilizzare nell&#39;elenco dei modelli (la definizione completa di questo nodo non è elencata sopra - è più semplice copiare un&#39;istanza di thumbnail.png da un report esistente).

### Creazione di un&#39;istanza del nuovo report {#creating-an-instance-of-your-new-report}

È ora possibile creare un&#39;istanza del nuovo rapporto:

1. Aprire la console **Strumenti**.

1. Selezionare **Reports** nel riquadro a sinistra.
1. Quindi **Nuovo...** dalla barra degli strumenti. Definite un **Titolo** e **Nome**, selezionate il nuovo tipo di rapporto (il **modello di rapporto OSGi**) dall&#39;elenco dei modelli, quindi fate clic su **Crea**.
1. La nuova istanza di report verrà visualizzata nell&#39;elenco. Fate doppio clic su questo per aprire.
1. Trascinate un componente (ad esempio, **Bundle** nel gruppo **OSGi Report**) dalla barra laterale per creare la prima colonna e [avviare la definizione del rapporto](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >Poiché in questo esempio non sono presenti colonne raggruppabili, i grafici non saranno disponibili. Per visualizzare i grafici, impostare `groupable` su `true`:
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## Configurazione dei servizi del framework di report {#configuring-the-report-framework-services}

Questa sezione descrive le opzioni di configurazione avanzate per i servizi OSGi che implementano il framework dei report.

Per visualizzarli, utilizzate il menu Configurazione della console Web (disponibile ad esempio in `http://localhost:4502/system/console/configMgr`). Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

### Servizio di base (configurazione di generazione rapporti di CQ Day) {#basic-service-day-cq-reporting-configuration}

* **** Timezonedefinisce i dati storici relativi al fuso orario per cui vengono creati. In questo modo, il grafico storico visualizzerà gli stessi dati per ogni utente in tutto il mondo.
* **** Localedefinisce le impostazioni internazionali da utilizzare insieme a  **** Timezoneper i dati storici. Le impostazioni internazionali vengono utilizzate per determinare alcune impostazioni di calendario specifiche per le impostazioni internazionali, ad esempio se il primo giorno di una settimana è domenica o lunedì.

* **Il** percorso dell&#39;istantanea definisce il percorso principale in cui sono memorizzate le istantanee dei grafici storici.
* **Il percorso dei** rapporti definisce il percorso in cui si trovano i rapporti. Questo viene utilizzato dal servizio di snapshot per determinare i report per i quali eseguire effettivamente delle istantanee.
* **Gli** snapshot giornalieri definiscono l&#39;ora di ogni giorno in cui vengono scattate le istantanee giornaliere. L&#39;ora specificata è nel fuso orario locale del server.
* **Gli** snapshot orari definiscono il minuto di ogni ora in cui vengono scattate le istantanee orari.
* **Righe (max)** definisce il numero massimo di righe memorizzate per ogni snapshot. Tale valore dovrebbe essere scelto in modo ragionevole; se è troppo alto, questo influirà sulle dimensioni del repository, se troppo basso, i dati potrebbero non essere precisi a causa del modo in cui vengono gestiti i dati storici.
* **I dati** falsi, se attivati, possono essere creati falsi dati storici utilizzando il  `fakedata` selettore; se disabilitato, l&#39;utilizzo del  `fakedata` selettore genererà un&#39;eccezione.

   Poiché i dati sono falsi, devono essere utilizzati *solo* a scopo di test e debug.

   Se si utilizza il selettore `fakedata`, il rapporto viene completato in modo implicito, in modo che tutti i dati esistenti vadano persi; i dati possono essere ripristinati manualmente, ma questo può richiedere molto tempo.

* **L’** utente delle istantanee definisce un utente facoltativo che può essere utilizzato per scattare delle istantanee.

   In sostanza, vengono effettuate istantanee per l’utente che ha completato il rapporto. Potrebbero verificarsi situazioni (ad esempio in un sistema di pubblicazione, in cui l’utente non esiste in quanto il suo account non è stato replicato) in cui si desidera specificare un utente fallback da utilizzare.

   Inoltre, la specifica di un utente potrebbe comportare un rischio per la sicurezza.

* **Applica agli utenti** snapshot, se abilitata, tutte le istantanee verranno scattate con l&#39;utente specificato in Utente ** snapshot. Questo potrebbe avere gravi conseguenze sulla sicurezza se non gestito correttamente.

### Impostazioni cache (cache di reporting di CQ giorno) {#cache-settings-day-cq-reporting-cache}

* **Abilita** consente di abilitare o disabilitare la memorizzazione nella cache dei dati del rapporto. Se si abilita la cache dei report, i dati dei report rimarranno in memoria durante diverse richieste. Ciò può migliorare le prestazioni, ma comporta un maggiore consumo di memoria e, in circostanze estreme, può causare una perdita di memoria.
* **TTL** definisce il tempo (in secondi) per il quale i dati del rapporto vengono memorizzati nella cache. Un numero più elevato aumenterà le prestazioni, ma potrebbe anche restituire dati imprecisi se i dati cambiano nel periodo di tempo.
* **Il numero massimo di** voci definisce il numero massimo di rapporti da memorizzare nella cache alla volta.

>[!NOTE]
>
>I dati del rapporto possono essere diversi per ciascun utente e lingua. Pertanto, i dati del rapporto sono memorizzati nella cache per rapporto, utente e lingua. Ciò significa che un valore **Max entry** di `2` memorizza nella cache i dati per:
>
>* un rapporto per due utenti con impostazioni di lingua diverse
>* un utente e due rapporti

>



