---
title: Blueprint SPA
description: Il presente documento descrive il contratto generale, indipendente dal quadro, che qualsiasi quadro dell'SPA dovrebbe soddisfare per attuare le componenti dell'SPA modificabili all'interno dell'AEM.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 6d961456e0e1f7a26121da9be493308a62c53e04
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 0%

---


# Blueprint SPA{#spa-blueprint}

Per consentire all’autore di utilizzare l’Editor SPA dell’AEM per modificare il contenuto di un SPA, l’SPA deve soddisfare alcuni requisiti descritti in questo documento.

{{ue-over-spa}}

## Introduzione {#introduction}

Il presente documento descrive il contratto generale che qualsiasi quadro SPA dovrebbe rispettare (ossia il tipo di livello di supporto AEM) per implementare componenti SPA modificabili all&#39;interno dell&#39;AEM.

>[!NOTE]
>
>I seguenti requisiti sono indipendenti dal framework. Se questi requisiti sono soddisfatti, è possibile fornire un livello specifico del framework composto da moduli, componenti e servizi.
>
>**Questi requisiti sono già soddisfatti per i framework React e Angular nell&#39;AEM.** I requisiti di questo blueprint sono rilevanti solo se si desidera implementare un altro framework per l&#39;utilizzo con AEM.

>[!CAUTION]
>
>Sebbene le capacità dell’AEM in materia di SPA siano indipendenti dal quadro, attualmente sono supportati solo i quadri React e Angular.

Per consentire all’autore di utilizzare l’Editor pagina AEM per modificare i dati esposti da un framework di applicazione a pagina singola, un progetto deve essere in grado di interpretare la struttura del modello che rappresenta la semantica dei dati memorizzati per un’applicazione all’interno dell’archivio AEM. Per raggiungere questo obiettivo, sono fornite due librerie indipendenti dal framework: `PageModelManager` e `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

La libreria `PageModelManager` viene fornita come pacchetto NPM da utilizzare per un progetto SPA. Accompagna l&#39;SPA e funge da gestore del modello di dati.

Per conto dell’SPA, astrae il recupero e la gestione della struttura JSON che rappresenta l’effettiva struttura del contenuto. È anche responsabile della sincronizzazione con l&#39;SPA per comunicare quando deve rieseguire il rendering dei suoi componenti.

Visualizza il pacchetto NPM [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

Durante l&#39;inizializzazione di `PageModelManager`, la libreria carica innanzitutto il modello radice fornito dell&#39;app (tramite il parametro, la proprietà meta o l&#39;URL corrente). Se la libreria identifica che il modello della pagina corrente non fa parte del modello principale che recupera e lo include come modello di una pagina figlio.

![modello_pagina_consolidamento](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

Il modulo `ComponentMapping` viene fornito come pacchetto NPM al progetto front-end. Memorizza i componenti front-end e consente all’SPA di mappare i componenti front-end ai tipi di risorse AEM. Ciò abilita una risoluzione dinamica dei componenti durante l’analisi del modello JSON dell’applicazione.

Ogni elemento presente nel modello contiene un campo `:type` che espone un tipo di risorsa AEM. Una volta montato, il componente front-end può eseguire il rendering utilizzando il frammento di modello ricevuto dalle librerie sottostanti.

#### Mappatura di un modello dinamico a un componente {#dynamic-model-to-component-mapping}

Per informazioni dettagliate sulla mappatura del modello dinamico ai componenti in JavaScript SPA SDK for AEM, vedere l&#39;articolo [Mappatura del modello dinamico ai componenti per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### Livello specifico del framework {#framework-specific-layer}

È necessario implementare un terzo livello per ogni framework front-end. Questa terza libreria è responsabile dell’interazione con le librerie sottostanti e fornisce una serie di punti di ingresso ben integrati e di facile utilizzo per l’interazione con il modello di dati.

Il resto del presente documento descrive i requisiti di questo livello specifico del quadro intermedio e aspira ad essere indipendente dal quadro. Nel rispetto dei seguenti requisiti, è possibile fornire un livello specifico per il framework affinché i componenti del progetto interagiscano con le librerie sottostanti incaricate di gestire il modello di dati.

## Concetti generali {#general-concepts}

### Modello pagina {#page-model}

La struttura del contenuto della pagina è memorizzata in AEM. Il modello della pagina viene utilizzato per mappare e creare istanze dei componenti SPA. Gli sviluppatori dell&#39;SPA creano i componenti dell&#39;SPA che mappano ai componenti dell&#39;AEM. A tal fine, utilizzano il tipo di risorsa (o il percorso del componente AEM) come chiave univoca.

I componenti SPA devono essere sincronizzati con il modello della pagina e devono essere aggiornati di conseguenza con qualsiasi modifica al relativo contenuto. Un pattern che utilizza componenti dinamici deve essere utilizzato per creare istantaneamente istanze di componenti seguendo la struttura del modello di pagina fornita.

### Meta campi {#meta-fields}

Il modello di pagina utilizza il modulo di esportazione del modello JSON, a sua volta basato sull&#39;API [Sling Model](https://sling.apache.org/documentation/bundles/models.html). I modelli sling esportabili espongono il seguente elenco di campi per consentire alle librerie sottostanti di interpretare il modello di dati:

* `:type`: tipo di risorsa AEM (predefinito = tipo di risorsa)
* `:children`: figli gerarchici della risorsa corrente. Gli elementi figlio non fanno parte del contenuto interno della risorsa corrente (sono disponibili negli elementi che rappresentano una pagina)
* `:hierarchyType`: tipo gerarchico di una risorsa. `PageModelManager` attualmente supporta il tipo di pagina

* `:items`: risorse di contenuto figlio della risorsa corrente (struttura nidificata, presente solo nei contenitori)
* `:itemsOrder`: elenco ordinato dei figli. L’oggetto mappa JSON non garantisce l’ordine dei relativi campi. Grazie alla mappa e all’array corrente, il consumatore dell’API beneficia di entrambe le strutture
* `:path`: percorso contenuto di un elemento (presente negli elementi che rappresentano una pagina)

Consulta anche [Guida introduttiva di AEM Content Services.](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### Modulo specifico per framework {#framework-specific-module}

Separare i dubbi aiuta a facilitare l’implementazione del progetto. Pertanto, è necessario fornire un pacchetto specifico per npm. Questo pacchetto è responsabile dell’aggregazione e dell’esposizione dei moduli, dei servizi e dei componenti di base. Questi componenti devono incapsulare la logica di gestione del modello dati e fornire accesso ai dati previsti dal componente del progetto. Il modulo è anche responsabile dell’esposizione transitiva di utili punti di ingresso delle librerie sottostanti.

Adobe Per facilitare l’interoperabilità delle librerie, consiglia al modulo specifico per il framework di raggruppare le seguenti librerie. Se necessario, il livello può incapsulare e adattare le API sottostanti prima di esporle al progetto.

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### Implementazioni {#implementations}

#### React {#react}

modulo npm: [@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

modulo npm: [@adobe/aem-angular-editable-components](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## Principali servizi e componenti {#main-services-and-components}

I seguenti organismi dovrebbero essere attuati conformemente agli orientamenti specifici di ciascun quadro. In base all’architettura del framework, l’implementazione può variare notevolmente, ma è necessario fornire le funzionalità descritte.

### Provider di modelli {#the-model-provider}

I componenti del progetto devono delegare l’accesso ai frammenti di un modello a un provider di modelli. Il provider di modelli è quindi incaricato di ascoltare le modifiche apportate al frammento specificato del modello e restituire il modello aggiornato al componente delegato.

Per eseguire questa operazione, il provider di modelli deve registrarsi in ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. Quindi, quando si verifica una modifica, riceve e trasmette i dati aggiornati al componente delegato. Per convenzione, la proprietà resa disponibile al componente delegato che conterrà il frammento del modello è denominata `cqModel`. L’implementazione è libera di fornire questa proprietà al componente, ma deve considerare aspetti quali l’integrazione con l’architettura del framework, la possibilità di individuare e la facilità d’uso.

### Il componente HTML Decorator {#the-component-html-decorator}

Il Component Decorator è responsabile della decorazione delle HTML esterne dell’elemento di ogni istanza del componente con una serie di attributi di dati e nomi di classi previsti dall’Editor pagina.

#### Dichiarazione del componente {#component-declaration}

I metadati seguenti devono essere aggiunti all’elemento HTML esterno prodotto dal componente del progetto. Consentono all’Editor pagina di recuperare la configurazione di modifica corrispondente.

* `data-cq-data-path`: percorso della risorsa relativo a `jcr:content`

#### Modifica della dichiarazione di capacità e del segnaposto {#editing-capability-declaration-and-placeholder}

I metadati e i nomi di classi seguenti devono essere aggiunti all&#39;elemento HTML esterno prodotto dal componente del progetto. Consentono all’Editor pagina di offrire funzionalità correlate.

* `cq-placeholder`: nome della classe che identifica il segnaposto per un componente vuoto
* `data-emptytext`: etichetta che deve essere visualizzata dalla sovrapposizione quando un&#39;istanza del componente è vuota

**Segnaposto per componenti vuoti**

Ogni componente deve essere esteso con una funzionalità che decorerà l’elemento HTML esterno con attributi di dati e nomi di classi specifici per segnaposto e sovrapposizioni correlate quando il componente viene identificato come vuoto.

**Informazioni sul valore vuoto di un componente**

* Il componente è logicamente vuoto?
* Qual è l’etichetta visualizzata dalla sovrapposizione quando il componente è vuoto?

### Contenitore {#container}

Un contenitore è un componente destinato a contenere ed eseguire il rendering dei componenti figlio. A tale scopo, il contenitore scorre le proprietà `:itemsOrder`, `:items` e `:children` del relativo modello.

Il contenitore ottiene dinamicamente i componenti figlio dall&#39;archivio della libreria [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping). Il contenitore estende quindi il componente secondario con le funzionalità del provider di modelli e infine lo crea come istanza.

### Pagina {#page}

Il componente `Page` estende il componente `Container`. Un contenitore è un componente destinato a contenere ed eseguire il rendering dei componenti figlio, incluse le pagine figlie. A tale scopo, il contenitore scorre le proprietà `:itemsOrder`, `:items` e `:children` del relativo modello. Il componente `Page` ottiene dinamicamente i componenti figlio dall&#39;archivio della libreria [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping). `Page` è responsabile della creazione delle istanze dei componenti figlio.

### Griglia reattiva {#responsive-grid}

Il componente Griglia reattiva è un contenitore. Contiene una variante specifica del provider di modelli che rappresenta le relative colonne. La griglia reattiva e le sue colonne sono responsabili della decorazione dell’elemento HTML esterno del componente del progetto con i nomi di classi specifici contenuti nel modello.

Il componente Griglia reattiva deve essere pre-mappato alla sua controparte AEM, in quanto è complesso e raramente personalizzato.

#### Campi modello specifici {#specific-model-fields}

* `gridClassNames:` Nomi di classe forniti per la griglia reattiva
* `columnClassNames:` Nomi di classe forniti per la colonna reattiva

#### Segnaposto della griglia reattiva {#placeholder-of-the-reponsive-grid}

Il componente SPA è mappato a un contenitore grafico come la griglia reattiva e deve aggiungere un segnaposto figlio virtuale durante la creazione del contenuto. Quando il contenuto dell&#39;SPA viene creato dall&#39;Editor pagina, tale contenuto viene incorporato nell&#39;editor utilizzando un iframe e l&#39;attributo `data-cq-editor` viene aggiunto al nodo del documento di tale contenuto. Se l&#39;attributo `data-cq-editor` è presente, il contenitore deve includere un elemento HTMLlement per rappresentare l&#39;area con cui l&#39;autore interagisce quando inserisce un nuovo componente nella pagina.

Ad esempio:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>I nomi delle classi utilizzati nell’esempio sono attualmente richiesti dall’editor di pagine.
>
>* `"new section"`: indica che l&#39;elemento corrente è il segnaposto del contenitore
>* `"aem-Grid-newComponent"`: normalizza il componente per la creazione del layout
>

#### Mappatura dei componenti {#component-mapping}

La libreria [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) sottostante e la relativa funzione `MapTo` possono essere incapsulate ed estese per fornire le funzionalità relative alla configurazione di modifica fornita insieme alla classe del componente corrente.

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

Nell&#39;implementazione di cui sopra, il componente del progetto viene esteso con la funzionalità di vuoto prima che venga effettivamente registrato nell&#39;archivio [Mappatura componenti](/help/sites-developing/spa-blueprint.md#componentmapping). Questa operazione viene eseguita incapsulando ed estendendo la libreria [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) per introdurre il supporto dell&#39;oggetto di configurazione `EditConfig`:

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## Contrarre con l’Editor pagina {#contract-with-the-page-editor}

I componenti del progetto devono generare almeno i seguenti attributi di dati per consentire all’editor di interagire con essi.

* `data-cq-data-path`: percorso relativo del componente fornito da `PageModel` (ad esempio, `"root/responsivegrid/image"`). Questo attributo non deve essere aggiunto alle pagine.

In sintesi, per essere interpretato dall’editor pagina come modificabile, un componente di progetto deve rispettare il seguente contratto:

* Specifica gli attributi previsti per associare un’istanza del componente front-end a una risorsa AEM.
* Fornisci la serie prevista di attributi e nomi di classi che consente la creazione di segnaposto vuoti.
* Specifica i nomi di classe previsti per consentire il trascinamento della selezione delle risorse.

### Struttura tipica degli elementi HTML {#typical-html-element-structure}

Il frammento seguente illustra la tipica rappresentazione HTML di una struttura del contenuto di una pagina. Di seguito sono riportati alcuni punti importanti:

* L&#39;elemento griglia reattivo contiene nomi di classe con prefisso `aem-Grid--`
* L&#39;elemento della colonna reattivo contiene nomi di classe con prefisso `aem-GridColumn--`
* Viene racchiusa una griglia reattiva che è anche la colonna di una griglia padre, ad esempio i due prefissi precedenti non vengono visualizzati sullo stesso elemento
* Gli elementi corrispondenti alle risorse modificabili contengono una proprietà `data-cq-data-path`. Consulta la sezione [Contratto con Editor pagina](#contract-wtih-the-page-editor) di questo documento.

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## Navigazione e indirizzamento {#navigation-and-routing}

L&#39;app è proprietaria del routing. Lo sviluppatore front-end deve innanzitutto implementare un componente Navigazione (mappato a un componente Navigazione AEM). Questo componente esegue il rendering dei collegamenti URL da utilizzare insieme a una serie di route che visualizzano o nascondono frammenti di contenuto.

La libreria [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) sottostante e il relativo modulo ` [ModelRouter](/help/sites-developing/spa-routing.md)` (abilitato per impostazione predefinita) sono responsabili della preacquisizione e dell&#39;accesso al modello associato a un determinato percorso di risorsa.

Le due entità si riferiscono alla nozione di routing, ma ` [ModelRouter](/help/sites-developing/spa-routing.md)` è responsabile solo del caricamento di ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` con un modello dati strutturato in sincronia con lo stato corrente dell&#39;applicazione.

Per ulteriori informazioni, vedere l&#39;articolo [Routing modello SPA](/help/sites-developing/spa-routing.md).

## SPA in azione {#spa-in-action}

Scopri come funziona un semplice SPA e come sperimentare autonomamente un SPA continuando a consultare il documento [Guida introduttiva all&#39;SPA nell&#39;AEM](/help/sites-developing/spa-getting-started-react.md).

## Ulteriori informazioni {#further-reading}

Per maggiori informazioni sull’SPA nell’AEM, consulta i seguenti documenti:

* [Panoramica sull&#39;authoring dell&#39;SPA](/help/sites-developing/spa-overview.md) per una panoramica dell&#39;SPA nell&#39;AEM e del modello di comunicazione
* [Guida introduttiva all&#39;SPA nell&#39;AEM](/help/sites-developing/spa-getting-started-react.md) per una guida a un SPA semplice e al suo funzionamento
