---
title: Sviluppo di rapporti
description: Adobe Experience Manager (AEM) fornisce una selezione di rapporti standard basati su un framework di reporting
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '5177'
ht-degree: 0%

---


# Sviluppo di rapporti {#developing-reports}

Adobe Experience Manager (AEM) fornisce una selezione di [report standard](/help/sites-administering/reporting.md), la maggior parte dei quali si basa su un framework di reporting.

Utilizzando il framework è possibile estendere questi rapporti standard o sviluppare nuovi rapporti personalizzati. Il framework di reporting si integra strettamente con i concetti e i principi CQ5 esistenti in modo che gli sviluppatori possano utilizzare le loro conoscenze esistenti di CQ5 come trampolino di lancio per lo sviluppo di rapporti.

Per le relazioni standard trasmesse con l’AEM:

* Questi rapporti si basano sul framework di reporting:

   * [Report componente](/help/sites-administering/reporting.md#component-report)
   * [Report attività pagina](/help/sites-administering/reporting.md#page-activity-report)
   * [Report utente](/help/sites-administering/reporting.md#user-report)
   * [Report di istanze flusso di lavoro](/help/sites-administering/reporting.md#workflow-instance-report)

* Le seguenti relazioni si basano su singoli principi e pertanto non possono essere estese:

   * [Utilizzo disco](/help/sites-administering/reporting.md#disk-usage)
   * [Verifica stato](/help/sites-administering/reporting.md#health-check)
   * [Report di workflow](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>L&#39;esercitazione [Creazione di un proprio report - Un esempio](#creating-your-own-report-an-example) mostra anche quanti dei principi riportati di seguito possono essere utilizzati.
>
>Puoi anche fare riferimento ai rapporti standard per visualizzare altri esempi di implementazione.

>[!NOTE]
>
>Negli esempi e nelle definizioni che seguono viene utilizzata la seguente notazione:
>
>* Ogni riga definisce un nodo o una proprietà in cui:
>  `N:<name> [<nodeType>]` : descrive un nodo con il nome `<*name*>` e il tipo di nodo `<*nodeType*>`*.*
>  `P:<name> [<propertyType]` : descrive una proprietà con il nome `<*name*>` e un tipo di proprietà `<*propertyType*>`.
>  `P:<name> = <value>` : descrive una proprietà `<name>` che deve essere impostata sul valore di `<value>`.
>
>* Il rientro mostra le dipendenze gerarchiche tra i nodi.
>* Elementi separati da | denota un elenco di elementi possibili, ad esempio tipi o nomi; ad esempio, `String|String[]` significa che la proprietà può essere String o String[].
>
>* `[]` rappresenta un array, ad esempio String[] o un array di nodi, come nella [Definizione query](#query-definition).
>
>Salvo diversa indicazione, i tipi predefiniti sono:
>
>* Nodi - `nt:unstructured`
>* Proprietà - `String`

## Framework di reporting {#reporting-framework}

Il quadro di riferimento per le relazioni si basa sui seguenti principi:

* È interamente basato su set di risultati restituiti da una query eseguita dal QueryBuilder CQ5.
* Il set di risultati definisce i dati visualizzati nel rapporto. Ogni riga del set di risultati corrisponde a una riga nella vista a tabella del rapporto.
* Le operazioni disponibili per l&#39;esecuzione nel set di risultati sono simili a concetti RDBMS; principalmente *raggruppamento* e *aggregazione*.

* La maggior parte del recupero e dell’elaborazione dei dati viene effettuata lato server.
* Il cliente è l’unico responsabile della visualizzazione dei dati preelaborati. Solo le attività di elaborazione minori (ad esempio, la creazione di collegamenti nel contenuto delle celle) vengono eseguite sul lato client.

Il framework di reporting (illustrato dalla struttura di un rapporto standard) utilizza i seguenti blocchi predefiniti, alimentati dalla coda di elaborazione:

![chlimage_1-248](assets/chlimage_1-248.png)

### Pagina report {#report-page}

La pagina del rapporto è:

* Una pagina CQ5 standard.
* Basato su un [modello CQ5 standard, configurato per il report](#report-template).

### Base rapporto {#report-base}

Il componente [`reportbase`](#report-base-component) costituisce la base di qualsiasi report perché:

* Mantiene la definizione della [query](#the-query-and-data-retrieval) che fornisce il set di risultati sottostante dei dati.

* È un sistema paragrafo adattato che contiene tutte le colonne ( `columnbase`) aggiunte al report.
* Definisce quali tipi di grafico sono disponibili e quali sono attualmente attivi.
* Definisce la finestra di dialogo Modifica, che consente all&#39;utente di configurare alcuni aspetti del report.

### Base colonna {#column-base}

Ogni colonna è un&#39;istanza del componente [`columnbase`](#column-base-component) che:

* È un paragrafo, utilizzato dal parsys ( `reportbase`) del rispettivo report.
* Definisce il collegamento al [set di risultati sottostante](#the-query-and-data-retrieval). In altre parole, definisce i dati specifici a cui si fa riferimento all’interno di questo set di risultati e il modo in cui vengono elaborati.
* Mantiene definizioni aggiuntive, ad esempio gli aggregati e i filtri disponibili, insieme a eventuali valori predefiniti.

### Query e recupero dati {#the-query-and-data-retrieval}

La query:

* È definito come parte del componente [`reportbase`](#report-base).
* È basato su [CQ QueryBuilder](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html).
* Recupera i dati utilizzati come base del rapporto. Ogni riga del set di risultati (tabella) è associata a un nodo come restituito dalla query. Le informazioni specifiche per [singole colonne](#column-base-component) vengono quindi estratte da questo set di dati.

* Di solito è costituito da:

   * Un percorso di directory principale.

     Specifica la sottostruttura del repository in cui eseguire la ricerca.

     Per ridurre al minimo l’impatto sulle prestazioni, è consigliabile (provare a) limitare la query a una sottostruttura specifica dell’archivio. Il percorso principale può essere predefinito nel [modello di report](#report-template) o impostato dall&#39;utente nella [finestra di dialogo Configurazione (Modifica)](#configuration-dialog).

   * [Uno o più criteri](#query-definition).

     Questi vengono imposti per produrre il set di risultati (iniziale); includono, ad esempio, restrizioni sul tipo di nodo o vincoli di proprietà.

**Il punto chiave è che ogni singolo nodo restituito nel set di risultati della query viene utilizzato per generare una singola riga nel report (quindi una relazione 1:1).**

Lo sviluppatore deve assicurarsi che la query definita per un report restituisca un set di nodi appropriato per quel report. Tuttavia, il nodo stesso non deve contenere tutte le informazioni richieste, che possono anche essere derivate dai nodi padre e/o figlio. Ad esempio, la query utilizzata per il [report utente](/help/sites-administering/reporting.md#user-report) seleziona i nodi in base al tipo di nodo (in questo caso `rep:user`). Tuttavia, la maggior parte delle colonne di questo report non prende i dati direttamente da questi nodi, ma dai nodi figlio `profile`.

### Coda di elaborazione {#processing-queue}

La [query](#the-query-and-data-retrieval) restituisce un set di risultati di dati da visualizzare come righe nel report. Ogni riga del set di risultati viene elaborata (lato server), in [diverse fasi](#phases-of-the-processing-queue), prima di essere trasferita al client per la visualizzazione nel report.

Ciò consente di:

* Estrazione e derivazione dei valori dal set di risultati sottostante.

  Ad esempio, ti consente di elaborare due valori di proprietà come un singolo valore calcolando la differenza tra i due.

* Risoluzione dei valori estratti; questa operazione può essere eseguita in vari modi.

  Ad esempio, è possibile mappare i percorsi a un titolo (come nel contenuto leggibile dalla persona della rispettiva proprietà *jcr:title*).

* Applicazione di filtri in vari punti.
* Se necessario, create i valori composti.

  Ad esempio, costituito da un testo visualizzato dall’utente, da un valore da utilizzare per l’ordinamento e da un URL aggiuntivo utilizzato (sul lato client) per la creazione di un collegamento.

#### Flusso di lavoro della coda di elaborazione {#workflow-of-the-processing-queue}

Il seguente flusso di lavoro rappresenta la coda di elaborazione:

![chlimage_1-249](assets/chlimage_1-249.png)

#### Fasi della coda di elaborazione {#phases-of-the-processing-queue}

Se le fasi e gli elementi dettagliati sono:

1. Trasforma i risultati restituiti dalla [query iniziale (reportbase)](#query-definition) nel set di risultati di base utilizzando gli estrattori di valori.

   Gli estrattori di valori vengono scelti automaticamente in base al tipo di colonna [](#column-specific-definitions). Vengono utilizzati per leggere i valori dalla query JCR sottostante e creare un set di risultati da essi; dopo di che è possibile applicare ulteriori elaborazioni. Ad esempio, per il tipo `diff`, l&#39;estrattore di valore legge due proprietà, calcola il singolo valore che viene quindi aggiunto al set di risultati. Impossibile configurare gli estrattori di valore.

1. A questo set di risultati iniziale, contenente dati non elaborati, viene applicato [filtro iniziale](#column-specific-definitions) (*fase raw*).

1. I valori sono [preelaborati](#processing-queue); come definito per la fase *applica*.

1. [Il filtro](#column-specific-definitions) (assegnato alla fase *preelaborato*) viene eseguito sui valori preelaborati.

1. I valori vengono risolti in base al [resolver definito](#processing-queue).
1. [Il filtro](#column-specific-definitions) (assegnato alla fase *resolved*) viene eseguito sui valori risolti.

1. I dati sono [raggruppati e aggregati](#column-specific-definitions).
1. I dati della matrice vengono risolti convertendoli in un elenco (basato su stringhe).

   Questo è un passaggio implicito che converte un risultato con più valori in un elenco che può essere visualizzato; è obbligatorio per i valori delle celle (non aggregati) basati su proprietà JCR con più valori.

1. I valori sono nuovamente [preelaborati](#processing-queue); come definito per la fase *afterApply*.

1. I dati sono ordinati.
1. I dati elaborati vengono trasferiti al client.

>[!NOTE]
>
>La query iniziale che restituisce il set di risultati dei dati di base è definita per il componente `reportbase`.
>
>Altri elementi della coda di elaborazione sono definiti nei componenti `columnbase`.

## Costruzione e configurazione dei rapporti {#report-construction-and-configuration}

Per creare e configurare un rapporto sono necessari i seguenti elementi:

* una [posizione per la definizione dei componenti del report](#location-of-report-components)
* un componente [`reportbase`](#report-base-component)
* uno o più [`columnbase` componenti](#column-base-component)
* un [componente pagina](#page-component)
* una [progettazione report](#report-design)
* un [modello di report](#report-template)

### Posizione dei componenti del rapporto {#location-of-report-components}

I componenti di reporting predefiniti sono contenuti in `/libs/cq/reporting/components`.

Tuttavia, si consiglia di non aggiornare questi nodi, ma di creare nodi di componenti personalizzati in `/apps/cq/reporting/components` o, se più appropriato, in `/apps/<yourProject>/reports/components`.

Dove (ad esempio):

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

In questo caso, puoi creare la directory principale del report e, sotto, il componente base del report e i componenti base della colonna:

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### Componente Pagina  {#page-component}

Una pagina di report deve utilizzare `sling:resourceType` di `/libs/cq/reporting/components/reportpage`.

Un componente pagina personalizzato non dovrebbe essere necessario (in genere).

## Componente base rapporto {#report-base-component}

Ogni tipo di report richiede un componente contenitore derivato da `/libs/cq/reporting/components/reportbase`.

Questo componente funge da contenitore per il rapporto nel suo complesso e fornisce informazioni per:

* La [definizione query](#query-definition).
* Finestra di dialogo [ (facoltativo)](#configuration-dialog) per la configurazione del report.
* Qualsiasi [grafico](#chart-definitions) integrato con il report.

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

  Limita il set di risultati ai nodi con proprietà specifiche con valori specifici. Se sono specificati più vincoli, il nodo deve soddisfare tutti (operazione AND).

  Ad esempio:

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

  Restituisce tutti i `textimage` componenti modificati per ultimi dall&#39;utente `admin`.

* `nodeTypes`

  Utilizzato per limitare il set di risultati ai tipi di nodo specificati. È possibile specificare più tipi di nodo.

* `mandatoryProperties`

  Limita il set di risultati ai nodi che hanno *tutti* le proprietà specificate. Il valore delle proprietà non è considerato per.

Tutti sono facoltativi e possono essere combinati in base alle necessità, ma è necessario definirne almeno uno.

### Definizioni del grafico {#chart-definitions}

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

     Poiché è possibile definire più impostazioni, è possibile utilizzarle per definire quali sono attualmente attive. Questi sono definiti da un array di nodi (non esiste alcuna convenzione di denominazione obbligatoria per questi nodi, ma i report standard utilizzano spesso `0`, `1`. `x`), ciascuno con la seguente proprietà:

      * `id`

        Identificazione dei grafici attivi. Deve corrispondere all&#39;ID di uno dei grafici `definitions`.

* `definitions`

  Definisce i tipi di grafico potenzialmente disponibili per il report. `definitions` da utilizzare è specificato dalle impostazioni `active`.

  Le definizioni vengono specificate utilizzando un array di nodi (di nuovo spesso denominati `0`, `1`). `x`), ciascuno con le seguenti proprietà:

   * `id`

     Identificazione del grafico.

   * `type`

     Tipo di grafico disponibile. Seleziona da:

      * `pie`
Grafico a torta. Generato solo dai dati correnti.

      * `lineseries`
Serie di linee (punti di collegamento che rappresentano gli snapshot effettivi). Generato solo da dati storici.

   * Sono disponibili proprietà aggiuntive, a seconda del tipo di grafico:

      * tipo di grafico `pie`:

         * `maxRadius` ( `Double/Long`)

           Raggio massimo consentito per il grafico a torta, quindi dimensione massima consentita per il grafico (senza legenda). Ignorato se `fixedRadius` è definito.

         * `minRadius` ( `Double/Long`)

           Raggio minimo consentito per il grafico a torta. Ignorato se `fixedRadius` è definito.

         * `fixedRadius` ( `Double/Long`)
Definisce un raggio fisso per il grafico a torta.

      * tipo di grafico [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

           True se deve essere visualizzata una riga aggiuntiva che mostra il **totale**.
predefinito: `false`

         * `series` ( `Long`)

           Numero di righe/serie da visualizzare.
predefinito: `9` (anche questo è il massimo consentito)

         * `hoverLimit` ( `Long`)

           Numero massimo di istantanee aggregate (punti visualizzati su ogni linea orizzontale, che rappresentano valori distinti) per le quali devono essere visualizzati i popup. ovvero quando l&#39;utente passa il mouse su un valore distinto o su un&#39;etichetta corrispondente nella legenda del grafico.

           impostazione predefinita: `35` (ovvero, non vengono visualizzati popup se sono applicabili più di 35 valori distinti per le impostazioni correnti del grafico).

           Esiste un limite aggiuntivo di dieci pop-up che possono essere visualizzati in parallelo (è possibile visualizzare più pop-up quando si passa il mouse sui testi delle legende).

### Finestra di dialogo di configurazione {#configuration-dialog}

Ogni rapporto può avere una finestra di dialogo di configurazione, che consente all’utente di specificare vari parametri per il rapporto. Questa finestra di dialogo è accessibile tramite il pulsante **Modifica** quando la pagina del report è aperta.

Questa finestra di dialogo è un CQ standard [dialog](/help/sites-developing/components-basics.md#dialogs) e può essere configurata come tale (vedi [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog) per ulteriori informazioni).

Di seguito è riportato un esempio di finestra di dialogo:

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

Sono forniti diversi componenti preconfigurati; è possibile fare riferimento a essi nella finestra di dialogo, utilizzando la proprietà `xtype` con un valore di `cqinclude`:

* **`title`**

  `/libs/cq/reporting/components/commons/title`

  Campo di testo per definire il titolo del rapporto.

* **`description`**

  `/libs/cq/reporting/components/commons/description`

  Area di testo per definire la descrizione del rapporto.

* **`processing`**

  `/libs/cq/reporting/components/commons/processing`

  Selettore per la modalità di elaborazione del rapporto (caricamento manuale/automatico dei dati).

* **`scheduling`**

  `/libs/cq/reporting/components/commons/scheduling`

  Selettore per la pianificazione di snapshot per il grafico cronologico.

>[!NOTE]
>
>I componenti a cui si fa riferimento devono essere inclusi utilizzando il suffisso `.infinity.json` (vedi l&#39;esempio precedente).

### Percorso directory principale {#root-path}

Inoltre, è possibile definire un percorso principale per il rapporto:

* **`rootPath`**

  Questo limita il report a una determinata sezione (albero o sottoalbero) dell’archivio, consigliata per l’ottimizzazione delle prestazioni. Il percorso principale è specificato dalla proprietà `rootPath` del nodo `report` di ogni pagina del report (ricavato dal modello al momento della creazione della pagina).

  Può essere specificato da:

   * il [modello di report](#report-template) (come valore fisso o predefinito per la finestra di dialogo di configurazione).
   * utente (utilizzando questo parametro)

## Componente base colonna {#column-base-component}

Ogni tipo di colonna richiede un componente derivato da `/libs/cq/reporting/components/columnbase`.

Un componente colonna definisce una combinazione dei seguenti elementi:

* Configurazione della query [specifica per colonna](#column-specific-query).
* [Resolver e pre-elaborazione](#resolvers-and-preprocessing).
* Le [definizioni specifiche della colonna](#column-specific-definitions) (ad esempio filtri e aggregati; `definitions` nodo figlio).
* [Valori predefiniti colonna](#column-default-values).
* [Client Filter](#client-filter) per estrarre le informazioni per la visualizzazione dai dati restituiti dal server.
* Inoltre, un componente colonna deve fornire un&#39;istanza appropriata di `cq:editConfig`. per definire gli [eventi e azioni](#events-and-actions) richiesti.
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

Vedi anche [Definizione del nuovo report](#defining-your-new-report).

### Query specifica per colonna {#column-specific-query}

Definisce l&#39;estrazione dei dati specifica (dal [set di risultati dei dati del report](#the-query-and-data-retrieval)) da utilizzare nella singola colonna.

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

  Se una proprietà è definita come String[], vengono analizzate più proprietà (in sequenza) per trovare il valore effettivo.

  Ad esempio, se è presente:

  `property = [ "jcr:lastModified", "jcr:created" ]`

  L’estrattore di valore corrispondente (che si trova qui sotto controllo):

   * Verifica se è disponibile una proprietà jcr:lastModified e, in tal caso, utilizzarla.
   * Se non è disponibile alcuna proprietà jcr:lastModified, viene utilizzato il contenuto di jcr:created.

* `subPath`

  Se il risultato non si trova nel nodo restituito dalla query, `subPath` definisce dove si trova la proprietà.

* `secondaryProperty`

  Una seconda proprietà che deve essere utilizzata per calcolare il valore effettivo della cella. Questa definizione viene utilizzata solo per alcuni tipi di colonna (differenze e ordinamento).

  Ad esempio, se è presente il rapporto Istanze flusso di lavoro, la proprietà specificata viene utilizzata per memorizzare il valore effettivo della differenza di tempo (in millisecondi) tra l&#39;ora di inizio e l&#39;ora di fine.

* `secondarySubPath`

  Simile a subPath, quando si utilizza `secondaryProperty`.

In genere, viene utilizzato solo `property`.

### Filtro client {#client-filter}

Il filtro client estrae le informazioni da visualizzare dai dati restituiti dal server.

>[!NOTE]
>
>Questo filtro viene eseguito lato client, dopo l’applicazione dell’intera elaborazione lato server.

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` è una funzione di JavaScript che:

* come input, riceve un parametro; i dati restituiti dal server (completamente preelaborati)
* come output, restituisce il valore filtrato (elaborato); i dati estratti o derivati dalle informazioni di input

L’esempio seguente estrae il percorso della pagina corrispondente da un percorso di componente:

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### Resolver e pre-elaborazione {#resolvers-and-preprocessing}

La [coda di elaborazione](#processing-queue) definisce i vari resolver e configura la preelaborazione:

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

     Associa i valori ad altri valori; ad esempio, viene utilizzato per risolvere costanti come `en` nel relativo valore equivalente `English`.

   * `default`

     Il resolver predefinito. Questo è un risolutore fittizio che in realtà non risolve nulla.

   * `page`

     Risolve un valore di percorso nel percorso della pagina appropriata; più precisamente, nel nodo `jcr:content` corrispondente. Ad esempio, `/content/.../page/jcr:content/par/xyz` è risolto in `/content/.../page/jcr:content`.

   * `path`

     Risolve un valore di percorso aggiungendo facoltativamente un percorso secondario e prendendo il valore effettivo da una proprietà del nodo (come definito da `resolverConfig`) nel percorso risolto. Ad esempio, è possibile risolvere `path` di `/content/.../page/jcr:content` nel contenuto della proprietà `jcr:title`, ciò significherebbe che un percorso di pagina viene risolto nel titolo della pagina.

   * `pathextension`

     Risolve un valore anteponendo un percorso e prendendo il valore effettivo da una proprietà del nodo nel percorso risolto. Ad esempio, un valore `de` potrebbe essere preceduto da un percorso come `/libs/wcm/core/resources/languages`, prendendo il valore dalla proprietà `language`, per risolvere il codice paese `de` nella descrizione della lingua `German`.

* `resolverConfig`

  Fornisce le definizioni per il resolver. Le opzioni disponibili dipendono da `resolver` selezionato:

   * `const`

     Utilizzare le proprietà per specificare le costanti per la risoluzione. Il nome della proprietà definisce la costante da risolvere; il valore della proprietà definisce il valore risolto.

     Ad esempio, una proprietà con **Name**= `1` e **Value** `=One` risolve 1 in 1.

   * `default`

     Nessuna configurazione disponibile.

   * `page`

      * `propertyName` (facoltativo)

        Definisce il nome della proprietà da utilizzare per la risoluzione del valore. Se non viene specificato, viene utilizzato il valore predefinito *jcr:title* (titolo della pagina). Per il risolutore `page`, ciò significa che prima il percorso viene risolto nel percorso della pagina, quindi ulteriormente risolto nel titolo della pagina.

   * `path`

      * `propertyName` (facoltativo)

        Specifica il nome della proprietà da utilizzare per la risoluzione del valore. Se non viene specificato, verrà utilizzato il valore predefinito `jcr:title`.

      * `subPath` (facoltativo)

        Questa proprietà può essere utilizzata per specificare un suffisso da aggiungere al percorso prima che il valore venga risolto.

   * `pathextension`

      * `path` (obbligatorio)

        Definisce il percorso da anteporre.

      * `propertyName` (obbligatorio)

        Definisce la proprietà nel percorso risolto in cui si trova il valore effettivo.

      * `i18n` (facoltativo; tipo booleano)

        Determina se il valore risolto deve essere *internazionalizzato* (ovvero, utilizzando i servizi di internazionalizzazione di [CQ5](/help/sites-administering/tc-manage.md)).

* `preprocessing`

  La preelaborazione è facoltativa e può essere associata (separatamente) alle fasi di elaborazione *apply* o *applyAfter*:

   * `apply`

     Fase di pre-elaborazione iniziale ([passaggio 3 nella rappresentazione della coda di elaborazione](#processing-queue)).

   * `applyAfter`

     Applica dopo la preelaborazione ([passaggio 9 nella rappresentazione della coda di elaborazione](#processing-queue)).

#### Resolver {#resolvers}

I resolver vengono utilizzati per estrarre le informazioni necessarie. Esempi dei vari risolutori sono:

**Const**

Di seguito viene risolto un valore costante di `VersionCreated` nella stringa `New version created`.

Vedere `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**Pagina**

Risolve un valore di percorso per la proprietà jcr:description nel nodo jcr:content (figlio) della pagina corrispondente.

Vedere `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**Percorso**

Di seguito viene risolto un percorso di `/content/.../page` nel contenuto della proprietà `jcr:title`. Ciò significa che un percorso di pagina viene risolto nel titolo della pagina.

Vedere `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**Estensione percorso**

Il valore seguente precede un valore `de` con l&#39;estensione del percorso `/libs/wcm/core/resources/languages`, quindi prende il valore dalla proprietà `language`, per risolvere il codice paese `de` nella descrizione della lingua `German`.

Vedere `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### Preelaborazione {#preprocessing}

La definizione `preprocessing` può essere applicata a:

* valore originale:

  La definizione di pre-elaborazione per il valore originale è specificata direttamente in `apply` e/o `applyAfter`.

* valore allo stato aggregato:

  Se necessario, è possibile fornire una definizione distinta per ciascuna aggregazione.

  Per specificare la pre-elaborazione esplicita per i valori aggregati, le definizioni di pre-elaborazione devono trovarsi su un rispettivo nodo figlio `aggregated` ( `apply/aggregated`, `applyAfter/aggregated`). Se è richiesta una preelaborazione esplicita per aggregati distinti, la definizione di preelaborazione si trova su un nodo figlio con il nome del rispettivo aggregato (ad esempio, `apply/aggregated/min/max` o altri aggregati).

È possibile specificare una delle seguenti opzioni da utilizzare durante la pre-elaborazione:

* [trova e sostituisci pattern](#preprocessing-find-and-replace-patterns)
Quando viene trovato, il pattern specificato (definito come espressione regolare) viene sostituito da un altro pattern; ad esempio, questo può essere utilizzato per estrarre una sottostringa dell’originale.

* [formattatori del tipo di dati](#preprocessing-data-type-formatters)

  Converte un valore numerico in una stringa relativa; ad esempio, il valore &quot;che rappresenta una differenza temporale di un&#39;ora viene risolto in una stringa come `1:24PM (1 hour ago)`.

Ad esempio:

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

Per la pre-elaborazione è possibile specificare un `pattern` (definito come [espressione regolare](https://en.wikipedia.org/wiki/Regular_expression) o regex) che si trova e quindi è sostituito dal pattern `replace`:

* `pattern`

  Espressione regolare utilizzata per individuare una sottostringa.

* `replace`

  Stringa, o rappresentazione della stringa, utilizzata come sostituzione della stringa originale. Spesso rappresenta una sottostringa della stringa che si trova nell&#39;espressione regolare `pattern`.

Un esempio di sostituzione può essere suddiviso come:

* Per il nodo `definitions/data/preprocessing/apply` con le due proprietà seguenti:

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* Stringa in arrivo come:

   * `/content/geometrixx/en/services/jcr:content/par/text`

* Suddiviso in quattro sezioni:

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* E sostituito con la stringa rappresentata da `$1`:

   * `/content/geometrixx/en/services`

#### Preelaborazione - Tipo di dati per gli argomenti {#preprocessing-data-type-formatters}

Questi formattatori convertono un valore numerico in una stringa relativa.

Ad esempio, può essere utilizzato per una colonna di tempo che consente di aggregare `min`, `avg` e `max`. Poiché gli aggregati `min`/ `avg`/ `max` vengono visualizzati come *differenza di tempo* (ad esempio, `10 days ago`), è necessario un formattatore dati. Per questo, un formattatore `datedelta` viene applicato ai valori aggregati `min`/ `avg`/ `max`. Se è disponibile anche un aggregato `count`, non è necessario un formattatore, né il valore originale.

Al momento i formattatori dei tipi di dati disponibili sono:

* `format`

  Formattatore tipo di dati:

   * `duration`

     La durata è l’intervallo di tempo tra due date definite. Ad esempio, l’inizio e la fine di un’azione del flusso di lavoro che ha richiesto un’ora, a partire dalle 11:23h del 2/13/11 e con termine un’ora dopo alle 12:23h del 2/13/11.

     Converte un valore numerico (interpretato come millisecondi) in una stringa di durata; ad esempio, `30000` è formattato come * `30s`.*

   * `datedelta`

     L’intervallo di tempo tra una data passata e &quot;ora&quot; è quindi diverso (se il rapporto viene visualizzato in un momento successivo).

     Converte il valore numerico (interpretato come differenza temporale in giorni) in una stringa di data relativa. Ad esempio, 1 è stato formattato come un giorno fa.

Nell&#39;esempio seguente viene definita la formattazione `datedelta` per gli aggregati `min` e `max`:

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

Le definizioni specifiche della colonna definiscono i filtri e gli aggregati disponibili per tale colonna.

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

  Di seguito sono riportate le opzioni standard disponibili:

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

     Utilizzato per estrarre parti di una data necessarie per l’aggregazione (ad esempio, raggruppare per anno per ottenere i dati aggregati per ogni anno).

   * `sortable`

     Utilizzato per valori che utilizzano valori diversi (come estratti da proprietà diverse) per l’ordinamento e la visualizzazione.

  Inoltre, qualsiasi valore di cui sopra può essere definito come multivalore; ad esempio, `string[]` definisce un array di stringhe.

  L&#39;estrattore di valore viene scelto dal tipo di colonna. Se per un tipo di colonna è disponibile un estrattore di valore, viene utilizzato tale estrattore. In caso contrario, viene utilizzato il valore di default dell&#39;estrattore.

  Un tipo può (facoltativamente) accettare un parametro. Ad esempio, `timeslot:year` estrae l&#39;anno da un campo data. Tipi con i relativi parametri:

   * `timeslot` - I valori sono paragonabili alle costanti corrispondenti di `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`

* `groupable`

  Definisce se il report può essere raggruppato per questa colonna.

* `filters`

  Definizioni dei filtri.

   * `filterType`

     I filtri disponibili sono:

      * `string`

        Un filtro basato su stringhe.

   * `id`

     Identificatore del filtro.

   * `phase`

     Fasi disponibili:

      * `raw`

        Il filtro viene applicato ai dati non elaborati.

      * `preprocessed`

        Il filtro viene applicato ai dati preelaborati.

      * `resolved`

        Il filtro viene applicato ai dati risolti.

* `aggregates`

  Definizioni aggregate.

   * `text`

     Nome testuale dell’aggregato. Se `text` non è specificato, verrà utilizzata la descrizione predefinita dell&#39;aggregato. Ad esempio, `minimum` viene utilizzato per l&#39;aggregato `min`.

   * `type`

     Tipo aggregato. Gli aggregati disponibili sono:

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

        Fornisce il valore mediano.

      * `percentile95`

        Utilizza il 95° percentile di tutti i valori.

### Valori predefiniti colonna {#column-default-values}

Definisce i valori predefiniti per la colonna:

```xml
N:defaults
    P:aggregate
```

* `aggregate`

  I valori `aggregate` validi sono gli stessi di `type` in `aggregates` (vedi [Definizioni specifiche delle colonne (definizioni - filtri / aggregati)](#column-specific-definitions) ).

### Eventi e azioni {#events-and-actions}

Modifica configurazione definisce gli eventi necessari che i listener devono rilevare e le azioni da applicare dopo che si sono verificati. Per informazioni generali, vedere l&#39;[introduzione allo sviluppo dei componenti](/help/sites-developing/components.md).

Devono essere definiti i seguenti valori per garantire che tutte le azioni richieste siano soddisfatte:

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

Le colonne generiche sono un’estensione in cui la maggior parte delle definizioni delle colonne è memorizzata nell’istanza del nodo della colonna (anziché nel nodo del componente).

Utilizzano una finestra di dialogo (standard) che potete personalizzare per il singolo componente generico. Questa finestra di dialogo consente all&#39;utente del report di definire le proprietà di una colonna generica nella pagina del report utilizzando l&#39;opzione di menu **Proprietà colonna...**.

Un esempio è la colonna **Generic** del **report utente**. Vedere `/libs/cq/reporting/components/userreport/genericcol`.

Per rendere una colonna generica:

* Impostare la proprietà `type` del nodo `definition` della colonna su `generic`.

  Vedi `/libs/cq/reporting/components/userreport/genericcol/definitions`

* Specifica una definizione di finestra di dialogo (standard) sotto il nodo `definition` della colonna.

  Vedi `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * I campi della finestra di dialogo devono fare riferimento agli stessi nomi della proprietà del componente corrispondente, incluso il relativo percorso.

     Ad esempio, se desideri che il tipo della colonna generica possa essere configurato tramite la finestra di dialogo, utilizza un campo con il nome `./definitions/type`.

   * Le proprietà definite tramite l&#39;interfaccia utente/la finestra di dialogo hanno la precedenza su quelle definite nel componente `columnbase`.

* Definisci la configurazione di modifica.

  Vedi `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* Utilizza metodologie AEM standard per definire proprietà di colonna (aggiuntive).

  Per le proprietà definite sia sulle istanze del componente che su quelle della colonna, il valore sull’istanza della colonna ha la precedenza.

  Le proprietà disponibili per una colonna generica sono:

   * `jcr:title` - nome colonna
   * `definitions/aggregates` - aggregati
   * `definitions/filters` - filtri
   * `definitions/type`- il tipo di colonna (deve essere definito nella finestra di dialogo, utilizzando un selettore/casella combinata o un campo nascosto)
   * `definitions/data/resolver` e `definitions/data/resolverConfig` (ma non `definitions/data/preprocessing` o `.../clientFilter`) - il resolver e la configurazione
   * `definitions/queryBuilder` - configurazione del generatore di query
   * `defaults/aggregate` - aggregato predefinito

  Se esiste una nuova istanza della colonna generica nel **report utente**, le proprietà definite nella finestra di dialogo vengono mantenute in:

  `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## Progettazione report {#report-design}

La progettazione definisce quali tipi di colonna sono disponibili per la creazione di un rapporto. Definisce inoltre il sistema paragrafo a cui vengono aggiunte le colonne.

L’Adobe consiglia di creare una singola progettazione per ogni rapporto. In questo modo si garantisce la massima flessibilità. Consulta [Definizione Del Nuovo Report](#defining-your-new-report).

I componenti di reporting predefiniti sono contenuti in `/etc/designs/reports`.

La posizione dei rapporti può dipendere dalla posizione dei componenti:

* `/etc/designs/reports/<yourReport>` è adatto se il report si trova in `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` per i report che utilizzano il pattern `/apps/<yourProject>/reports`

Le proprietà di progettazione richieste sono registrate in `jcr:content/reportpage/report/columns` (ad esempio, `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

  Qualsiasi componente e/o gruppo di componenti consentito nel rapporto.

* `sling:resourceType`

  Proprietà con valore `cq/reporting/components/repparsys`.

Un esempio di frammento di progettazione (tratto dalla progettazione del rapporto del componente) è:

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

Non è necessario specificare le progettazioni per le singole colonne. Le colonne disponibili possono essere definite in modalità progettazione.

>[!NOTE]
>
>L&#39;Adobe consiglia di non modificare le progettazioni standard dei rapporti. In questo modo, è possibile assicurarsi di non perdere le modifiche apportate durante l&#39;aggiornamento o l&#39;installazione degli hotfix.
>
>Copiare il report e la relativa struttura se si desidera personalizzare un report standard.

>[!NOTE]
>
>Le colonne predefinite possono essere create automaticamente durante la creazione di un report. Questi sono specificati nel modello.

## Modello di rapporto {#report-template}

Ogni tipo di rapporto deve fornire un modello. Si tratta di [modelli CQ standard](/help/sites-developing/templates.md) che possono essere configurati come tali.

Il modello deve:

* imposta `sling:resourceType` su `cq/reporting/components/reportpage`

* indicare il progetto da utilizzare
* crea un nodo figlio `report` che fa riferimento al componente contenitore ( `reportbase`) con la proprietà `sling:resourceType`

Un esempio di frammento di modello (tratto dal modello di report del componente) è:

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

Un esempio di frammento di modello, che mostra la definizione del percorso principale (tratto dal modello di report utente), è:

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

I modelli di reporting predefiniti si trovano in `/libs/cq/reporting/templates`.

Tuttavia, l’Adobe consiglia di non aggiornare questi nodi. Creare invece nodi di componenti personalizzati in `/apps/cq/reporting/templates` o se più appropriato in `/apps/<yourProject>/reports/templates`.

Dove, ad esempio (vedi anche [Posizione dei componenti report](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

In questo caso, crea la directory principale per il modello:

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## Creazione di un rapporto personalizzato: un esempio {#creating-your-own-report-an-example}

### Definizione del nuovo rapporto {#defining-your-new-report}

Per definire un rapporto, crea e configura:

1. La directory principale dei componenti del rapporto.
1. Il componente base del rapporto.
1. Uno o più componenti base per colonne.
1. Progettazione del report.
1. Directory principale del modello di report.
1. Il modello di report.

Per illustrare questi passaggi, l’esempio seguente definisce un rapporto che elenca tutte le configurazioni OSGi all’interno dell’archivio. Tutte le istanze del nodo `sling:OsgiConfig`.

>[!NOTE]
>
>Un metodo alternativo consiste nel copiare un rapporto esistente e poi personalizzare la nuova versione.

1. Crea il nodo principale per il nuovo rapporto.

   Ad esempio, in `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. Definire la base di rapporti. Ad esempio, `osgireport[cq:Component]` in `/apps/cq/reporting/components/osgireport`.

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

   Definisce un componente base per il rapporto che:

   * cerca tutti i nodi di tipo `sling:OsgiConfig`
   * visualizza entrambi i grafici `pie` e `lineseries`
   * fornisce una finestra di dialogo che consente all’utente di configurare il rapporto

1. Definisci il componente della prima colonna (columnbase). Ad esempio, `bundlecol[cq:Component]` in `/apps/cq/reporting/components/osgireport`.

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

   Definisce un componente columnbase che:

   * cerca e restituisce il valore ricevuto dal server; in questo caso la proprietà `jcr:path` per ogni nodo `sling:OsgiConfig`
   * fornisce l&#39;aggregato `count`
   * non è raggruppabile
   * ha il titolo `Bundle` (titolo colonna nella tabella)
   * è nel gruppo di barra laterale `OSGi Report`
   * aggiorna in base agli eventi specificati

   >[!NOTE]
   >
   >In questo esempio non sono presenti definizioni di `N:data` e `P:clientFilter`. Questo perché il valore ricevuto dal server viene restituito in rapporto 1:1, che è il comportamento predefinito.
   >
   >Questo è lo stesso delle definizioni:
   >
   >```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >Dove la funzione restituisce semplicemente il valore ricevuto.

1. Definisci la struttura del rapporto. Ad esempio, `osgireport[cq:Page]` in `/etc/designs/reports`.

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

1. Definisci il modello di rapporto. Ad esempio, `osgireport[cq:Template]` in `/apps/cq/reporting/templates`.

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create an OSGi report."
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

   Questo definisce un modello che:

   * definisce `allowedPaths` per i report risultanti - nel caso precedente, ovunque sotto `/etc/reports`
   * fornisce titoli e descrizioni per il modello
   * fornisce un’immagine miniatura da utilizzare nell’elenco dei modelli (la definizione completa di questo nodo non è elencata sopra; è più semplice copiare un’istanza di thumbnail.png da un rapporto esistente).

### Creazione di un’istanza del nuovo rapporto {#creating-an-instance-of-your-new-report}

È ora possibile creare un’istanza del nuovo rapporto:

1. Apri la console **Strumenti**.

1. Selezionare **Report** nel riquadro di sinistra.
1. Quindi **Nuovo...** dalla barra degli strumenti. Definisci un **Titolo** e un **Nome**, seleziona il nuovo tipo di rapporto (il **Modello di rapporto OSGi**) dall&#39;elenco dei modelli, quindi fai clic su **Crea**.
1. La nuova istanza di report viene visualizzata nell’elenco. Fare doppio clic per aprire.
1. Trascina un componente (per questo esempio, **Bundle** nel gruppo **Report OSGi**) dalla barra laterale per creare la prima colonna e [avviare la definizione del report](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >Poiché questo esempio non contiene colonne raggruppabili, i grafici non sono disponibili. Per visualizzare i grafici, impostare `groupable` su `true`:
   >
   >```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```
   >

## Configurazione dei servizi di Report Framework {#configuring-the-report-framework-services}

In questa sezione vengono descritte le opzioni di configurazione avanzate per i servizi OSGi che implementano il framework di report.

Questi possono essere visualizzati utilizzando il menu Configuration della console Web (disponibile ad esempio in `http://localhost:4502/system/console/configMgr`). Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le procedure consigliate.

### Servizio di base (configurazione di reporting Day CQ) {#basic-service-day-cq-reporting-configuration}

* **Il fuso orario** definisce il fuso orario per il quale vengono creati i dati storici. In questo modo, il grafico cronologico mostrerà gli stessi dati per ogni utente in tutto il mondo.
* **Impostazioni locali** definisce le impostazioni locali da utilizzare con **Fuso orario** per i dati storici. Le impostazioni internazionali vengono utilizzate per determinare alcune impostazioni di calendario specifiche delle impostazioni internazionali, ad esempio se il primo giorno della settimana è domenica o lunedì.

* **Percorso snapshot** definisce il percorso principale in cui vengono archiviati gli snapshot per i grafici cronologici.
* **Percorso dei report** definisce il percorso in cui si trovano i report. Viene utilizzato dal servizio snapshot per determinare i report per i quali eseguire effettivamente le snapshot.
* **Snapshot giornalieri** definisce l&#39;ora di ogni giorno in cui vengono eseguiti gli snapshot giornalieri. L&#39;ora specificata si trova nel fuso orario locale del server.
* **Snapshot orari** definisce il minuto di ogni ora in cui vengono eseguiti gli snapshot orari.
* **Righe (max)** definisce il numero massimo di righe archiviate per ogni snapshot. Questo valore dovrebbe essere scelto in modo ragionevole. Se è troppo alta, influisce sulle dimensioni dell’archivio; se è troppo bassa, i dati potrebbero non essere accurati a causa del modo in cui vengono gestiti i dati storici.
* **Dati falsi**, se abilitata, è possibile creare dati storici falsi utilizzando il selettore `fakedata`. Se disabilitata, l&#39;utilizzo del selettore `fakedata` genera un&#39;eccezione.

  Poiché i dati sono falsi, è necessario utilizzarli *solo* a scopo di test e debug.

  L&#39;utilizzo del selettore `fakedata` termina il report in modo implicito, quindi tutti i dati esistenti vengono persi. I dati possono essere ripristinati manualmente, ma questo processo può richiedere tempo.

* **Utente snapshot** definisce un utente facoltativo che può essere utilizzato per creare snapshot.

  In pratica, vengono create istantanee per l&#39;utente che ha terminato il report. In alcuni casi (ad esempio, in un sistema di pubblicazione in cui l’utente non esiste in quanto l’account non è stato replicato) puoi specificare un utente di fallback da utilizzare in alternativa.

  Inoltre, la specifica di un utente potrebbe comportare un rischio per la sicurezza.

* **Applica utente snapshot**, se attivato, tutti gli snapshot vengono creati con l&#39;utente specificato in *Utente snapshot*. Questo potrebbe avere un grave impatto sulla sicurezza se non viene gestito correttamente.

### Impostazioni cache (Day CQ Reporting Cache) {#cache-settings-day-cq-reporting-cache}

* **Abilita** consente di abilitare o disabilitare la memorizzazione nella cache dei dati del report. L’abilitazione della cache dei rapporti mantiene i dati del rapporto in memoria durante diverse richieste. Questo può aumentare le prestazioni, ma porta a un maggiore consumo di memoria e, in circostanze estreme, può portare a situazioni di memoria insufficiente.
* **TTL** definisce il tempo (in secondi) per il quale i dati del report vengono memorizzati nella cache. Un numero più elevato migliora le prestazioni, ma può anche restituire dati imprecisi se i dati cambiano entro il periodo di tempo.
* **Max. voci** definisce il numero massimo di report da memorizzare nella cache contemporaneamente.

>[!NOTE]
>
>I dati dei rapporti possono essere diversi per ogni utente e lingua. Pertanto, i dati del rapporto vengono memorizzati nella cache per report, utente e lingua. Ciò significa che un valore **Max entry** di `2` memorizza effettivamente nella cache i dati per:
>
>* un rapporto per due utenti con impostazioni di lingua diverse
>* un utente e due rapporti
>
