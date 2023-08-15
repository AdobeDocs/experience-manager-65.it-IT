---
title: Sviluppo di rapporti
seo-title: Developing Reports
description: L'AEM fornisce una selezione di rapporti standard basati su un framework di reporting
seo-description: AEM provides a selection of standard reports based on a reporting framework
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '5239'
ht-degree: 0%

---


# Sviluppo di rapporti {#developing-reports}

L&#39;AEM offre una selezione di [rapporti standard](/help/sites-administering/reporting.md) la maggior parte di essi si basa su un framework di reporting.

Utilizzando il framework è possibile estendere questi rapporti standard o sviluppare rapporti personalizzati completamente nuovi. Il framework di reporting si integra strettamente con i concetti e i principi CQ5 esistenti in modo che gli sviluppatori possano utilizzare le loro conoscenze esistenti di CQ5 come trampolino di lancio per lo sviluppo di rapporti.

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
>Esercitazione [Creazione di un rapporto personalizzato: un esempio](#creating-your-own-report-an-example) mostra anche quanti dei principi riportati di seguito possono essere utilizzati.
>
>Puoi anche fare riferimento ai rapporti standard per visualizzare altri esempi di implementazione.

>[!NOTE]
>
>Negli esempi e nelle definizioni che seguono viene utilizzata la seguente notazione:
>
>* Ogni riga definisce un nodo o una proprietà in cui:
>  `N:<name> [<nodeType>]` : descrive un nodo denominato `<*name*>` e tipo di nodo di `<*nodeType*>`*.*
>  `P:<name> [<propertyType]` : descrive una proprietà denominata `<*name*>` e un tipo di proprietà di `<*propertyType*>`.
>  `P:<name> = <value>` : descrive una proprietà `<name>` che deve essere impostato sul valore di `<value>`.
>
>* Il rientro mostra le dipendenze gerarchiche tra i nodi.
>* Elementi separati da | indica un elenco di elementi possibili; ad esempio tipi o nomi; ad esempio, `String|String[]` indica che la proprietà può essere String o String[].
>
>* `[]` rappresenta un array, ad esempio Stringa[] o un array di nodi come in [Definizione query](#query-definition).
>
>Salvo diversa indicazione, i tipi predefiniti sono:
>
>* Nodi - `nt:unstructured`
>* Proprietà - `String`

## Framework di reporting {#reporting-framework}

Il quadro di riferimento per le relazioni si basa sui seguenti principi:

* È interamente basato su set di risultati restituiti da una query eseguita dal QueryBuilder CQ5.
* Il set di risultati definisce i dati visualizzati nel rapporto. Ogni riga del set di risultati corrisponde a una riga nella vista a tabella del rapporto.
* Le operazioni disponibili per l&#39;esecuzione sul set di risultati assomigliano a concetti RDBMS; principalmente *raggruppamento* e *aggregazione*.

* La maggior parte del recupero e dell’elaborazione dei dati viene effettuata sul server.
* Il cliente è l’unico responsabile della visualizzazione dei dati preelaborati. Solo le attività di elaborazione minori (ad esempio, la creazione di collegamenti nel contenuto delle celle) vengono eseguite sul lato client.

Il framework di reporting (illustrato dalla struttura di un rapporto standard) utilizza i seguenti blocchi predefiniti, alimentati dalla coda di elaborazione:

![chlimage_1-248](assets/chlimage_1-248.png)

### Pagina report {#report-page}

La pagina del rapporto:

* È una pagina CQ5 standard.
* È basato su un [modello CQ5 standard, configurato per il rapporto](#report-template).

### Base rapporto {#report-base}

Il [`reportbase` componente](#report-base-component) costituisce la base di qualsiasi rapporto in quanto:

* Contiene la definizione di [query](#the-query-and-data-retrieval) che fornisce il set di risultati sottostante dei dati.

* È un sistema paragrafo adattato che conterrà tutte le colonne ( `columnbase`) aggiunto al report.
* Definisce quali tipi di grafico sono disponibili e quali sono attualmente attivi.
* Definisce la finestra di dialogo Modifica, che consente all’utente di configurare alcuni aspetti del rapporto.

### Base colonna {#column-base}

Ogni colonna è un’istanza del [`columnbase` componente](#column-base-component) che:

* È un paragrafo, utilizzato dal parsys ( `reportbase`) della rispettiva relazione.
* Definisce il collegamento al [set di risultati sottostante](#the-query-and-data-retrieval), ovvero definisce i dati specifici a cui si fa riferimento in questo set di risultati e il modo in cui vengono elaborati.
* Contiene definizioni aggiuntive, ad esempio gli aggregati e i filtri disponibili, insieme a eventuali valori predefiniti.

### Query e recupero dati {#the-query-and-data-retrieval}

La query:

* è definito come parte della [`reportbase`](#report-base) componente.
* È basato su [CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html).
* Recupera i dati utilizzati come base del rapporto. Ogni riga del set di risultati (tabella) è associata a un nodo come restituito dalla query. Informazioni specifiche per [singole colonne](#column-base-component) viene quindi estratto da questo set di dati.

* Di solito è costituito da:

   * Un percorso di directory principale.

     Specifica la sottostruttura del repository in cui eseguire la ricerca.

     Per ridurre al minimo l’impatto sulle prestazioni, è consigliabile (provare a) limitare la query a una sottostruttura specifica dell’archivio. Il percorso della directory principale può essere predefinito nel [modello di report](#report-template) o impostato dall’utente in [Finestra di dialogo Configurazione (Modifica)](#configuration-dialog).

   * [Uno o più criteri](#query-definition).

     Questi vengono imposti per produrre il set di risultati (iniziale); includono, ad esempio, restrizioni sul tipo di nodo o vincoli di proprietà.

**Il punto chiave in questo caso è che ogni singolo nodo restituito nel set di risultati della query viene utilizzato per generare una singola riga sul report (quindi una relazione 1:1).**

Lo sviluppatore deve assicurarsi che la query definita per un report restituisca un set di nodi appropriato per quel report. Tuttavia, il nodo stesso non deve necessariamente contenere tutte le informazioni richieste, che possono anche essere derivate dai nodi padre e/o figlio. Ad esempio, la query utilizzata per [Report utente](/help/sites-administering/reporting.md#user-report) seleziona i nodi in base al tipo di nodo (in questo caso `rep:user`). Tuttavia, la maggior parte delle colonne in questo report non prende i propri dati direttamente da questi nodi, ma dai nodi figlio `profile`.

### Coda di elaborazione {#processing-queue}

Il [query](#the-query-and-data-retrieval) restituisce un set di risultati di dati da visualizzare come righe nel report. Ogni riga del set di risultati viene elaborata (lato server), in [diverse fasi](#phases-of-the-processing-queue), prima di essere trasferito al client per la visualizzazione nel report.

Ciò consente di:

* Estrazione e derivazione dei valori dal set di risultati sottostante.

  Ad esempio, ti consente di elaborare due valori di proprietà come un singolo valore calcolando la differenza tra i due.

* Risoluzione dei valori estratti; questa operazione può essere eseguita in diversi modi.

  Ad esempio, i percorsi possono essere mappati su un titolo (come nel contenuto più leggibile degli *jcr:title* proprietà ).

* Applicazione di filtri in vari punti.
* Se necessario, create i valori composti.

  Ad esempio, costituito da un testo visualizzato dall’utente, da un valore da utilizzare per l’ordinamento e da un URL aggiuntivo utilizzato (sul lato client) per la creazione di un collegamento.

#### Flusso di lavoro della coda di elaborazione {#workflow-of-the-processing-queue}

Il seguente flusso di lavoro rappresenta la coda di elaborazione:

![chlimage_1-249](assets/chlimage_1-249.png)

#### Fasi della coda di elaborazione {#phases-of-the-processing-queue}

Se le fasi e gli elementi dettagliati sono:

1. Trasforma i risultati restituiti da [query iniziale (reportbase)](#query-definition) nel set di risultati di base utilizzando gli estrattori di valore.

   Gli estrattori di valore vengono scelti automaticamente in base al [tipo di colonna](#column-specific-definitions). Vengono utilizzati per leggere i valori dalla query JCR sottostante e creare un set di risultati da essi; dopo di che è possibile applicare ulteriori elaborazioni. Ad esempio, per `diff` testo, l&#39;estrattore di valore legge due proprietà, calcola il singolo valore che viene quindi aggiunto al set di risultati. Impossibile configurare gli estrattori di valore.

1. A tale set di risultati iniziale, contenente dati non elaborati, [filtro iniziale](#column-specific-definitions) (*raw* fase di sviluppo).

1. I valori sono [pre-elaborato](#processing-queue); come definito per *applica* fase.

1. [Filtraggio](#column-specific-definitions) (assegnato al *pre-elaborato* fase) viene eseguito sui valori preelaborati.

1. I valori vengono risolti in base alla [resolver definito](#processing-queue).
1. [Filtraggio](#column-specific-definitions) (assegnato al *risolto* fase) viene eseguito sui valori risolti.

1. I dati sono [raggruppati e aggregati](#column-specific-definitions).
1. I dati della matrice vengono risolti convertendoli in un elenco (basato su stringhe).

   Questo è un passaggio implicito che converte un risultato con più valori in un elenco che può essere visualizzato; è obbligatorio per i valori delle celle (non aggregati) basati su proprietà JCR con più valori.

1. I valori sono di nuovo [pre-elaborato](#processing-queue); come definito per *afterApply* fase.

1. I dati sono ordinati.
1. I dati elaborati vengono trasferiti al client.

>[!NOTE]
>
>La query iniziale che restituisce il set di risultati dei dati di base è definita nel `reportbase` componente.
>
>Altri elementi della coda di elaborazione sono definiti nella `columnbase` componenti.

## Costruzione e configurazione dei rapporti {#report-construction-and-configuration}

Per creare e configurare un rapporto sono necessari i seguenti elementi:

* a [posizione per la definizione dei componenti del rapporto](#location-of-report-components)
* a [`reportbase` componente](#report-base-component)
* uno o più, [`columnbase` componente/i](#column-base-component)
* a [componente pagina](#page-component)
* a [progettazione report](#report-design)
* a [modello di report](#report-template)

### Posizione dei componenti del rapporto {#location-of-report-components}

Le componenti di reporting predefinite sono detenute sotto `/libs/cq/reporting/components`.

Tuttavia, si consiglia vivamente di non aggiornare questi nodi, ma di creare nodi di componenti personalizzati in `/apps/cq/reporting/components` o se più appropriato `/apps/<yourProject>/reports/components`.

Dove (ad esempio):

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

Sotto si crea la radice per il report e sotto a questo, il componente base del report e i componenti base della colonna:

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

Un componente pagina personalizzato non dovrebbe essere necessario (nella maggior parte dei casi).

## Componente base rapporto {#report-base-component}

Ogni tipo di report richiede un componente contenitore derivato da `/libs/cq/reporting/components/reportbase`.

Questo componente funge da contenitore per il rapporto nel suo complesso e fornisce informazioni per:

* Il [definizione query](#query-definition).
* Un [(facoltativo) finestra di dialogo](#configuration-dialog) per la configurazione del rapporto.
* Qualsiasi [Grafici](#chart-definitions) integrato nel rapporto.

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

  Può essere utilizzato per limitare il set di risultati a nodi con proprietà specifiche con valori specifici. Se sono specificati più vincoli, il nodo deve soddisfare tutti (operazione AND).

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

  Restituirebbe tutto `textimage` componenti che sono stati modificati l’ultima volta da `admin` utente.

* `nodeTypes`

  Utilizzato per limitare il set di risultati ai tipi di nodo specificati. È possibile specificare più tipi di nodo.

* `mandatoryProperties`

  Può essere utilizzato per limitare il set di risultati ai nodi che hanno *tutto* delle proprietà specificate. Il valore delle proprietà non viene preso in considerazione.

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

     Poiché è possibile definire più impostazioni, è possibile utilizzarle per definire quali sono attualmente attive. Questi sono definiti da un array di nodi (non esiste una convenzione di denominazione obbligatoria per questi nodi, ma i rapporti standard utilizzano spesso `0`, `1`.. `x`), aventi ciascuna le seguenti proprietà:

      * `id`

        Identificazione dei grafici attivi. Deve corrispondere all’ID di uno dei grafici `definitions`.

* `definitions`

  Definisce i tipi di grafico potenzialmente disponibili per il report. Il `definitions` da utilizzare sarà specificato da `active` impostazioni.

  Le definizioni vengono specificate utilizzando un array di nodi (di nuovo spesso denominati `0`, `1`.. `x`), ciascuno dei quali presenta le seguenti proprietà:

   * `id`

     Identificazione del grafico.

   * `type`

     Tipo di grafico disponibile. Seleziona da:

      * `pie`
Grafico a torta. Generato solo dai dati correnti.

      * `lineseries`
Serie di linee (punti di collegamento che rappresentano gli snapshot effettivi). Generato solo da dati storici.

   * Sono disponibili proprietà aggiuntive, a seconda del tipo di grafico:

      * per il tipo di grafico `pie`:

         * `maxRadius` ( `Double/Long`)

           Raggio massimo consentito per il grafico a torta, quindi dimensione massima consentita per il grafico (senza legenda). Ignorato se `fixedRadius` è definito.

         * `minRadius` ( `Double/Long`)

           Raggio minimo consentito per il grafico a torta. Ignorato se `fixedRadius` è definito.

         * `fixedRadius` ( `Double/Long`) Definisce un raggio fisso per il grafico a torta.

      * per il tipo di grafico [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

           True se viene visualizzata una riga aggiuntiva contenente **Totale** devono essere visualizzati.
impostazione predefinita: `false`

         * `series` ( `Long`)

           Numero di righe/serie da visualizzare.
impostazione predefinita: `9` (questo è anche il massimo consentito)

         * `hoverLimit` ( `Long`)

           Numero massimo di istantanee aggregate (punti visualizzati su ogni linea orizzontale, che rappresentano valori distinti) per le quali devono essere visualizzate le finestre a comparsa, ovvero quando l’utente passa il puntatore del mouse su un valore distinto o su un’etichetta corrispondente nella legenda del grafico.

           impostazione predefinita: `35` (ovvero non vengono visualizzate finestre a comparsa se sono applicabili più di 35 valori distinti per le impostazioni correnti del grafico).

           Esiste un limite aggiuntivo di 10 popup che possono essere visualizzati in parallelo (è possibile visualizzare più popup quando si passa il mouse sopra i testi delle legende).

### Finestra di dialogo di configurazione {#configuration-dialog}

Ogni rapporto può avere una finestra di dialogo di configurazione, che consente all’utente di specificare vari parametri per il rapporto. Questa finestra di dialogo è accessibile tramite **Modifica** quando la pagina del report è aperta.

Questa finestra di dialogo è un CQ standard [finestra di dialogo](/help/sites-developing/components-basics.md#dialogs) e può essere configurato come tale (vedi [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) per ulteriori informazioni).

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

Sono disponibili diversi componenti preconfigurati a cui è possibile fare riferimento nella finestra di dialogo utilizzando `xtype` proprietà con valore `cqinclude`:

* **`title`**

  `/libs/cq/reporting/components/commons/title`

  Campo di testo per definire il titolo del rapporto.

* **`description`**

  `/libs/cq/reporting/components/commons/description`

  Textarea per definire la descrizione del report.

* **`processing`**

  `/libs/cq/reporting/components/commons/processing`

  Selettore per la modalità di elaborazione del rapporto (caricamento manuale/automatico dei dati).

* **`scheduling`**

  `/libs/cq/reporting/components/commons/scheduling`

  Selettore per la pianificazione di snapshot per il grafico cronologico.

>[!NOTE]
>
>I componenti di riferimento devono essere inclusi utilizzando `.infinity.json` (vedi esempio precedente).

### Percorso directory principale {#root-path}

Inoltre, è possibile definire un percorso principale per il rapporto:

* **`rootPath`**

  Questo limita il report a una determinata sezione (albero o sottoalbero) dell’archivio, consigliata per l’ottimizzazione delle prestazioni. Il percorso della directory principale è specificato da `rootPath` proprietà del `report` di ogni pagina di rapporto (tratto dal modello al momento della creazione della pagina).

  Può essere specificato da:

   * il [modello di report](#report-template) (come valore fisso o predefinito per la finestra di dialogo di configurazione).
   * utente (utilizzando questo parametro)

## Componente base colonna {#column-base-component}

Ogni tipo di colonna richiede un componente derivato da `/libs/cq/reporting/components/columnbase`.

Un componente colonna definisce una combinazione dei seguenti elementi:

* Il [Query specifica per colonna](#column-specific-query) configurazione.
* Il [Resolver e pre-elaborazione](#resolvers-and-preprocessing).
* Il [Definizioni specifiche delle colonne](#column-specific-definitions) (ad esempio filtri e aggregati; `definitions` nodo figlio).
* [Valori predefiniti colonna](#column-default-values).
* Il [Filtro client](#client-filter) per estrarre le informazioni da visualizzare dai dati restituiti dal server.
* Inoltre, un componente colonna deve fornire un’istanza appropriata di `cq:editConfig`. per definire [Eventi e azioni](#events-and-actions) obbligatorio.
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

Vedi anche [Definizione del nuovo rapporto](#defining-your-new-report).

### Query specifica per colonna {#column-specific-query}

Questo definisce l’estrazione di dati specifica (dalla [set di risultati dei dati del rapporto](#the-query-and-data-retrieval)) da utilizzare nelle singole colonne.

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

  Se la proprietà è definita come stringa[] vengono analizzate più proprietà (in sequenza) per trovare il valore effettivo.

  Ad esempio:

  `property = [ "jcr:lastModified", "jcr:created" ]`

  L’estrattore di valore corrispondente (che si trova qui sotto controllo):

   * Verifica se è disponibile una proprietà jcr:lastModified e, in tal caso, utilizzala.
   * Se non è disponibile alcuna proprietà jcr:lastModified, verrà utilizzato il contenuto di jcr:created.

* `subPath`

  Se il risultato non si trova sul nodo restituito dalla query, `subPath` definisce dove si trova effettivamente la proprietà.

* `secondaryProperty`

  Definisce una seconda proprietà che deve essere utilizzata anche per calcolare il valore effettivo della cella. Questa proprietà verrà utilizzata solo per alcuni tipi di colonna (differenze e ordinamento).

  Ad esempio, nel caso del rapporto Istanze flusso di lavoro, la proprietà specificata viene utilizzata per memorizzare il valore effettivo della differenza di tempo (in millisecondi) tra l&#39;ora di inizio e l&#39;ora di fine.

* `secondarySubPath`

  Simile a subPath, quando `secondaryProperty` viene utilizzato.

Nella maggior parte dei casi, solo `property` verrà utilizzato.

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

`clientFilter` è definita come una funzione JavaScript che:

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

Il [coda di elaborazione](#processing-queue) definisce i vari risolutori e configura la preelaborazione:

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

     Mappa i valori su altri valori; ad esempio, viene utilizzato per risolvere costanti come `en` al suo valore equivalente `English`.

   * `default`

     Il resolver predefinito. Questo è un risolutore fittizio che in realtà non risolve nulla.

   * `page`

     Risolve un valore di percorso per il percorso della pagina appropriata; più precisamente, per il corrispondente `jcr:content` nodo. Ad esempio: `/content/.../page/jcr:content/par/xyz` è risolto in `/content/.../page/jcr:content`.

   * `path`

     Risolve un valore di percorso aggiungendo facoltativamente un percorso secondario e prendendo il valore effettivo da una proprietà del nodo (come definito da `resolverConfig`) nel percorso risolto. Ad esempio, un `path` di `/content/.../page/jcr:content` può essere risolto nel contenuto del `jcr:title` , ciò significa che il percorso di una pagina viene risolto nel titolo della pagina.

   * `pathextension`

     Risolve un valore anteponendo un percorso e prendendo il valore effettivo da una proprietà del nodo nel percorso risolto. Ad esempio, un valore `de` potrebbe essere preceduto da un percorso come `/libs/wcm/core/resources/languages`, prendendo il valore dalla proprietà `language`, per risolvere il codice paese `de` alla descrizione della lingua `German`.

* `resolverConfig`

  Fornisce le definizioni per il resolver; le opzioni disponibili dipendono dal `resolver` selezionato:

   * `const`

     Utilizzare le proprietà per specificare le costanti per la risoluzione. Il nome della proprietà definisce la costante da risolvere; il valore della proprietà definisce il valore risolto.

     Ad esempio, una proprietà con **Nome**= `1` e **Valore** `=One` risolverà da 1 a 1.

   * `default`

     Nessuna configurazione disponibile.

   * `page`

      * `propertyName` (facoltativo)

        Definisce il nome della proprietà da utilizzare per la risoluzione del valore. Se non viene specificato, il valore predefinito è *jcr:title* (titolo della pagina); per `page` resolver, significa che prima il percorso viene risolto nel percorso della pagina, quindi ulteriormente risolto nel titolo della pagina.

   * `path`

      * `propertyName` (facoltativo)

        Specifica il nome della proprietà da utilizzare per la risoluzione del valore. Se non viene specificato, il valore predefinito è `jcr:title` viene utilizzato.

      * `subPath` (facoltativo)

        Questa proprietà può essere utilizzata per specificare un suffisso da aggiungere al percorso prima che il valore venga risolto.

   * `pathextension`

      * `path` (obbligatorio)

        Definisce il percorso da anteporre.

      * `propertyName` (obbligatorio)

        Definisce la proprietà nel percorso risolto in cui si trova il valore effettivo.

      * `i18n` (facoltativo; tipo booleano)

        Determina se il valore risolto deve essere *internazionalizzato* (ovvero utilizzando [Servizi di internazionalizzazione di CQ5](/help/sites-administering/tc-manage.md)).

* `preprocessing`

  La pre-elaborazione è facoltativa e può essere associata (separatamente) alle fasi di elaborazione *applica* o *applyAfter*:

   * `apply`

     Fase di pre-elaborazione iniziale ([passaggio 3 nella rappresentazione della coda di elaborazione](#processing-queue)).

   * `applyAfter`

     Applica dopo la pre-elaborazione ([passaggio 9 nella rappresentazione della coda di elaborazione](#processing-queue)).

#### Resolver {#resolvers}

I resolver vengono utilizzati per estrarre le informazioni necessarie. Esempi dei vari risolutori sono:

**Const**

Di seguito viene descritto come risolvere un valore costante di `VersionCreated` alla stringa `New version created`.

Consulta `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**Pagina**

Risolve un valore di percorso per la proprietà jcr:description nel nodo jcr:content (figlio) della pagina corrispondente.

Consulta `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**Percorso**

Di seguito viene risolto un percorso di `/content/.../page` al contenuto del `jcr:title` , ciò significa che il percorso di una pagina viene risolto nel titolo della pagina.

Consulta `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**Estensione percorso**

Di seguito è riportato un valore preceduto da `de` con l’estensione del percorso `/libs/wcm/core/resources/languages`, quindi prende il valore dalla proprietà `language`, per risolvere il codice paese `de` alla descrizione della lingua `German`.

Consulta `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### Preelaborazione {#preprocessing}

Il `preprocessing` La definizione può essere applicata:

* valore originale:

  La definizione di pre-elaborazione per il valore originale è specificata in `apply` e/o `applyAfter` direttamente.

* valore allo stato aggregato:

  Se necessario, è possibile fornire una definizione distinta per ciascuna aggregazione.

  Per specificare una pre-elaborazione esplicita per i valori aggregati, le definizioni di pre-elaborazione devono trovarsi su un `aggregated` nodo figlio ( `apply/aggregated`, `applyAfter/aggregated`). Se è richiesta una preelaborazione esplicita per aggregati distinti, la definizione di preelaborazione si trova su un nodo figlio con il nome del rispettivo aggregato (ad esempio `apply/aggregated/min/max` o altri aggregati).

È possibile specificare una delle seguenti opzioni da utilizzare durante la pre-elaborazione:

* [trovare e sostituire i pattern](#preprocessing-find-and-replace-patterns)
Quando viene trovato, il pattern specificato (definito come espressione regolare) viene sostituito da un altro pattern; ad esempio, questo può essere utilizzato per estrarre una sottostringa dell’originale.

* [formattatori del tipo di dati](#preprocessing-data-type-formatters)

  Converte un valore numerico in una stringa relativa; ad esempio, il valore &quot;che rappresenta una differenza temporale di 1 ora viene risolto in una stringa come `1:24PM (1 hour ago)`.

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

Per la pre-elaborazione è possibile specificare `pattern` (definito come [espressione regolare](https://en.wikipedia.org/wiki/Regular_expression) o regex) che è localizzato e poi sostituito dal `replace` pattern:

* `pattern`

  Espressione regolare utilizzata per individuare una sottostringa.

* `replace`

  Stringa, o rappresentazione della stringa, che verrà utilizzata come sostituzione della stringa originale. Spesso rappresenta una sottostringa della stringa che si trova nell’espressione regolare `pattern`.

Un esempio di sostituzione può essere suddiviso come:

* Per il nodo `definitions/data/preprocessing/apply` con le due proprietà seguenti:

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* Stringa in arrivo come:

   * `/content/geometrixx/en/services/jcr:content/par/text`

* Sarà suddiviso in quattro sezioni:

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* E sostituito con la stringa rappresentata da `$1`:

   * `/content/geometrixx/en/services`

#### Preelaborazione - Tipo di dati per gli argomenti {#preprocessing-data-type-formatters}

Questi formattatori convertono un valore numerico in una stringa relativa.

Ad esempio, può essere utilizzato per una colonna di tempo che consente `min`, `avg` e `max` aggregati. As `min`/ `avg`/ `max` gli aggregati vengono visualizzati come *differenza di tempo* (ad esempio, `10 days ago`), richiedono un formattatore di dati. Per questo, un `datedelta` il formattatore viene applicato al `min`/ `avg`/ `max` valori aggregati. Se un `count` è disponibile anche l’aggregato, quindi non è necessario un formattatore, né il valore originale.

Al momento i formattatori dei tipi di dati disponibili sono:

* `format`

  Formattatore tipo di dati:

   * `duration`

     La durata è l’intervallo di tempo tra due date definite. Ad esempio, l’inizio e la fine di un’azione del flusso di lavoro che ha richiesto 1 ora, a partire dalle 11:23h del 2/13/11 e con fine un’ora dopo alle 12:23h del 2/13/11.

     Converte un valore numerico (interpretato come millisecondi) in una stringa di durata; ad esempio, `30000` è formattato come * `30s`.*

   * `datedelta`

     L’intervallo di tempo tra una data passata e &quot;ora&quot; è considerato diverso (in questo modo il risultato ottenuto sarà diverso se il rapporto viene visualizzato in un momento successivo).

     Converte il valore numerico (interpretato come differenza temporale in giorni) in una stringa di data relativa. Ad esempio, 1 è formattato come 1 giorno fa.

L’esempio che segue definisce `datedelta` formattazione per `min` e `max` aggregati:

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

     Viene utilizzato per estrarre parti di una data necessarie per l’aggregazione (ad esempio, raggruppare per anno per ottenere i dati aggregati per ogni anno).

   * `sortable`

     Viene utilizzato per valori che utilizzano valori diversi (come quelli ottenuti da proprietà diverse) per l’ordinamento e la visualizzazione.

  Inoltre. uno qualsiasi di questi può essere definito come valore multiplo; ad esempio, `string[]` definisce un array di stringhe.

  L&#39;estrattore di valore viene scelto dal tipo di colonna. Se per un tipo di colonna è disponibile un estrattore di valore, viene utilizzato tale estrattore. In caso contrario, viene utilizzato il valore di default dell&#39;estrattore.

  Un tipo può (facoltativamente) accettare un parametro. Ad esempio: `timeslot:year` estrae l’anno da un campo data. Tipi con i relativi parametri:

   * `timeslot` - I valori sono confrontabili con le costanti corrispondenti di `java.utils.Calendar`.

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

     Nome testuale dell’aggregato. Se `text` non è specificato, assumerà la descrizione predefinita dell’aggregato; ad esempio, `minimum` verrà utilizzato per `min` aggregato.

   * `type`

     Tipo aggregato. Gli aggregati disponibili sono:

      * `count`

        Conta il numero di righe.

      * `count-nonempty`

        Conta il numero di righe non vuote.

      * `min`

        Specifica il valore minimo.

      * `max`

        Specifica il valore massimo.

      * `average`

        Fornisce il valore medio.

      * `sum`

        Fornisce la somma di tutti i valori.

      * `median`

        Fornisce il valore mediano.

      * `percentile95`

        Prende il 95° percentile di tutti i valori.

### Valori predefiniti colonna {#column-default-values}

Viene utilizzato per definire i valori predefiniti per la colonna:

```xml
N:defaults
    P:aggregate
```

* `aggregate`

  Valido `aggregate` i valori sono gli stessi di `type` in `aggregates` (vedere [Definizioni specifiche per colonna (definizioni - filtri/aggregati)](#column-specific-definitions) ).

### Eventi e azioni {#events-and-actions}

Modifica configurazione definisce gli eventi necessari che i listener devono rilevare e le azioni da applicare dopo che si sono verificati. Consulta la [introduzione allo sviluppo di componenti](/help/sites-developing/components.md) per informazioni di base.

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

Utilizzano una finestra di dialogo (standard) che personalizzi per il singolo componente generico. Questa finestra di dialogo consente all&#39;utente del report di definire le proprietà di una colonna generica nella pagina del report utilizzando l&#39;opzione di menu **Proprietà colonna...**).

Un esempio è il **Generico** colonna del **Report utente**; vedi `/libs/cq/reporting/components/userreport/genericcol`.

Per rendere una colonna generica:

* Imposta il `type` proprietà della colonna `definition` nodo a `generic`.

  Consulta `/libs/cq/reporting/components/userreport/genericcol/definitions`

* Specifica una definizione di finestra di dialogo (standard) sotto il `definition` nodo.

  Consulta `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * I campi della finestra di dialogo devono fare riferimento agli stessi nomi della proprietà componente corrispondente (incluso il relativo percorso).

     Ad esempio, se desideri che il tipo della colonna generica possa essere configurato tramite la finestra di dialogo, utilizza un campo con il nome `./definitions/type`.

   * Le proprietà definite tramite l’interfaccia utente/la finestra di dialogo hanno la precedenza su quelle definite nella `columnbase` componente.

* Definisci la configurazione di modifica.

  Consulta `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* Utilizza metodologie AEM standard per definire proprietà di colonna (aggiuntive).

  Tieni presente che per le proprietà definite sia sulle istanze del componente che su quelle della colonna, il valore sull’istanza della colonna ha la precedenza.

  Le proprietà disponibili per una colonna generica sono:

   * `jcr:title` - nome colonna
   * `definitions/aggregates` - aggregati
   * `definitions/filters` - filtri
   * `definitions/type`- il tipo di colonna (deve essere definito nella finestra di dialogo, utilizzando un selettore o una casella combinata oppure un campo nascosto)
   * `definitions/data/resolver` e `definitions/data/resolverConfig` (ma non `definitions/data/preprocessing` o `.../clientFilter`) - il resolver e la configurazione
   * `definitions/queryBuilder` : configurazione del generatore di query
   * `defaults/aggregate` - aggregato predefinito

  Nel caso di una nuova istanza della colonna generica **Report utente** le proprietà definite con la finestra di dialogo vengono mantenute in:

  `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## Progettazione report {#report-design}

La progettazione definisce quali tipi di colonna sono disponibili per la creazione di un rapporto. Definisce inoltre il sistema paragrafo a cui vengono aggiunte le colonne.

Ti consigliamo vivamente di creare una singola progettazione per ogni rapporto. Questo assicura la massima flessibilità. Vedi anche [Definizione del nuovo rapporto](#defining-your-new-report).

Le componenti di reporting predefinite sono detenute sotto `/etc/designs/reports`.

La posizione dei rapporti può dipendere dalla posizione dei componenti:

* `/etc/designs/reports/<yourReport>` è adatto se il rapporto si trova in `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` per i rapporti che utilizzano `/apps/<yourProject>/reports` pattern

Le proprietà di progettazione richieste sono registrate il `jcr:content/reportpage/report/columns` (ad esempio, `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

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
>Si consiglia di non apportare modifiche alle progettazioni standard dei rapporti. In questo modo, è possibile assicurarsi di non perdere le modifiche apportate durante l&#39;aggiornamento o l&#39;installazione degli hotfix.
>
>Copiare il report e la relativa struttura se si desidera personalizzare un report standard.

>[!NOTE]
>
>Le colonne predefinite possono essere create automaticamente durante la creazione di un report. Questi sono specificati nel modello.

## Modello di rapporto {#report-template}

Ogni tipo di rapporto deve fornire un modello. Questi sono standard [Modelli CQ](/help/sites-developing/templates.md) e possono essere configurati come tali.

Il modello deve:

* imposta `sling:resourceType` a `cq/reporting/components/reportpage`

* indicare il progetto da utilizzare
* creare un `report` nodo figlio che fa riferimento al contenitore ( `reportbase`) per mezzo della `sling:resourceType` proprietà

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

I modelli di reporting predefiniti sono disponibili in `/libs/cq/reporting/templates`.

Tuttavia, si consiglia vivamente di non aggiornare questi nodi, ma di creare nodi di componenti personalizzati in `/apps/cq/reporting/templates` o se più appropriato `/apps/<yourProject>/reports/templates`.

Dove, ad esempio (vedi anche [Posizione dei componenti del rapporto](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

In questo è possibile creare la directory principale per il modello:

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## Creazione di un rapporto personalizzato: un esempio {#creating-your-own-report-an-example}

### Definizione del nuovo rapporto {#defining-your-new-report}

Per definire un nuovo rapporto è necessario creare e configurare:

1. La directory principale dei componenti del rapporto.
1. Il componente base del rapporto.
1. Uno o più componenti base per colonne.
1. Progettazione del report.
1. Directory principale del modello di report.
1. Il modello di report.

Per illustrare questi passaggi, l’esempio seguente definisce un rapporto che elenca tutte le configurazioni OSGi all’interno dell’archivio, ovvero tutte le istanze del `sling:OsgiConfig` nodo.

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

1. Definire la base di rapporti. Ad esempio `osgireport[cq:Component]` in `/apps/cq/reporting/components/osgireport`.

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
   * visualizza entrambi `pie` e `lineseries` grafici
   * fornisce una finestra di dialogo che consente all’utente di configurare il rapporto

1. Definisci il componente della prima colonna (columnbase). Ad esempio `bundlecol[cq:Component]` in `/apps/cq/reporting/components/osgireport`.

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

   Definisce un componente base per colonna che:

   * cerca e restituisce il valore ricevuto dal server; in questo caso la proprietà `jcr:path` per ogni `sling:OsgiConfig` nodo
   * fornisce `count` aggregato
   * non è raggruppabile
   * ha il titolo `Bundle` (titolo della colonna nella tabella)
   * è nel gruppo della barra laterale `OSGi Report`
   * aggiorna in base agli eventi specificati

   >[!NOTE]
   >
   >In questo esempio non ci sono definizioni di `N:data` e `P:clientFilter`. Questo perché il valore ricevuto dal server viene restituito in rapporto 1:1, che è il comportamento predefinito.
   >
   >Questo è lo stesso delle definizioni:
   >
   >```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >Dove la funzione restituisce semplicemente il valore che riceve.

1. Definisci la struttura del rapporto. Ad esempio `osgireport[cq:Page]` in `/etc/designs/reports`.

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

1. Definisci il modello di rapporto. Ad esempio `osgireport[cq:Template]` in `/apps/cq/reporting/templates`.

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

   Questo definisce un modello che:

   * definisce la `allowedPaths` per i rapporti risultanti: nel caso di cui sopra, in qualsiasi punto sotto `/etc/reports`
   * fornisce titoli e descrizioni per il modello
   * fornisce un’immagine miniatura da utilizzare nell’elenco dei modelli (la definizione completa di questo nodo non è elencata sopra; è più semplice copiare un’istanza di thumbnail.png da un rapporto esistente).

### Creazione di un’istanza del nuovo rapporto {#creating-an-instance-of-your-new-report}

È ora possibile creare un’istanza del nuovo rapporto:

1. Apri **Strumenti** console.

1. Seleziona **Rapporti** nel riquadro di sinistra.
1. Then **Nuovo...** dalla barra degli strumenti. Definisci un **Titolo** e **Nome**, seleziona il nuovo tipo di rapporto (il **Modello per report OSGi**) dall’elenco dei modelli, quindi fai clic su **Crea**.
1. La nuova istanza di report verrà visualizzata nell’elenco. Fare doppio clic per aprire.
1. Trascina un componente (per questo esempio: **Bundle** nel **Rapporto OSGi** ) dalla barra laterale per creare la prima colonna e [avvia la definizione del rapporto](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >Poiché questo esempio non contiene colonne raggruppabili, i grafici non saranno disponibili. Per visualizzare i grafici, impostare `groupable` a `true`:
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

Questi possono essere visualizzati utilizzando il menu Configuration della console web (disponibile ad esempio in `http://localhost:4502/system/console/configMgr`). Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le pratiche consigliate.

### Servizio di base (configurazione di reporting Day CQ) {#basic-service-day-cq-reporting-configuration}

* **Fuso orario** definisce il fuso orario per il quale vengono creati i dati storici. In questo modo, il grafico cronologico mostrerà gli stessi dati per ogni utente in tutto il mondo.
* **Lingua** definisce le impostazioni locali da utilizzare insieme al **Fuso orario** per i dati storici. Le impostazioni internazionali vengono utilizzate per determinare alcune impostazioni di calendario specifiche delle impostazioni internazionali, ad esempio se il primo giorno della settimana è domenica o lunedì.

* **Percorso snapshot** definisce il percorso principale in cui vengono archiviati gli snapshot per i grafici storici.
* **Percorso per i rapporti** definisce il percorso in cui si trovano i rapporti. Viene utilizzato dal servizio snapshot per determinare i report per i quali eseguire effettivamente le snapshot.
* **Snapshot giornalieri** definisce l&#39;ora di ogni giorno in cui vengono eseguite le istantanee giornaliere. L&#39;ora specificata si trova nel fuso orario locale del server.
* **Snapshot ogni ora** definisce il minuto di ogni ora in cui vengono eseguite le istantanee orarie.
* **Righe (max)** definisce il numero massimo di righe archiviate per ogni snapshot. Questo valore dovrebbe essere scelto in modo ragionevole; se è troppo alto, questo influirà sulle dimensioni dell’archivio; se è troppo basso, i dati potrebbero non essere accurati a causa del modo in cui vengono gestiti i dati storici.
* **Dati falsi**, se abilitata, è possibile creare dati storici falsi utilizzando `fakedata` ; se è disattivato, utilizza il `fakedata` Il selettore genera un’eccezione.

  Poiché i dati sono falsi, è necessario *solo* essere utilizzato a scopo di test e debug.

  Utilizzo di `fakedata` Il selettore finirà il rapporto in modo implicito, quindi tutti i dati esistenti andranno persi; i dati possono essere ripristinati manualmente, ma questo può richiedere molto tempo.

* **Utente snapshot** definisce un utente facoltativo che può essere utilizzato per creare snapshot.

  In pratica, vengono create istantanee per l&#39;utente che ha terminato il report. In alcune situazioni, ad esempio in un sistema di pubblicazione in cui l’utente non esiste in quanto l’account non è stato replicato, è possibile specificare un utente di fallback da utilizzare in alternativa.

  Inoltre, la specifica di un utente potrebbe comportare un rischio per la sicurezza.

* **Imponi utente snapshot**, se abilitata, tutte le istantanee verranno scattate con l&#39;utente specificato in *Utente snapshot*. Questo potrebbe avere gravi conseguenze sulla sicurezza se non viene gestito correttamente.

### Impostazioni cache (Day CQ Reporting Cache) {#cache-settings-day-cq-reporting-cache}

* **Abilita** consente di abilitare o disabilitare la memorizzazione nella cache dei dati del rapporto. L’abilitazione della cache dei rapporti manterrà i dati dei rapporti in memoria durante diverse richieste. Questo può aumentare le prestazioni, ma porta a un maggiore consumo di memoria e, in circostanze estreme, può portare a situazioni di memoria insufficiente.
* **TTL** definisce il tempo (in secondi) per il quale i dati del rapporto vengono memorizzati in cache. Un valore più alto migliora le prestazioni, ma può anche restituire dati imprecisi se i dati cambiano entro il periodo di tempo.
* **Max voci** definisce il numero massimo di rapporti da memorizzare in cache contemporaneamente.

>[!NOTE]
>
>I dati dei rapporti possono essere diversi per ogni utente e lingua. Pertanto, i dati del rapporto vengono memorizzati nella cache per report, utente e lingua. Ciò significa che **Max voci** valore di `2` memorizza nella cache i dati per:
>
>* un rapporto per due utenti con impostazioni di lingua diverse
>* un utente e due rapporti
>
