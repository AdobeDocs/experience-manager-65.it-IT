---
title: Blueprint SPA
seo-title: SPA Blueprint
description: Il presente documento descrive il contratto generale, indipendente dal quadro, che qualsiasi quadro SPA dovrebbe rispettare per attuare le componenti modificabili dell'SPA nell'ambito dell'AEM.
seo-description: This document describes the general, framework-independent contract that any SPA framework should fulfill in order to implement editable SPA components within AEM.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
source-git-commit: afd2afe182d65e64c0ad851b86021886078a9dd5
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 1%

---

# Blueprint SPA{#spa-blueprint}

Per consentire all’autore di utilizzare l’Editor SPA dell’AEM per modificare il contenuto di un SPA, l’SPA deve soddisfare alcuni requisiti descritti in questo documento.

>[!NOTE]
>
>L’editor SPA è la soluzione consigliata per i progetti che richiedono un rendering lato client basato sul framework SPA (ad esempio, React o Angular).

## Introduzione {#introduction}

Il presente documento descrive il contratto generale che qualsiasi quadro SPA dovrebbe rispettare (ossia il tipo di livello di sostegno dell&#39;AEM) al fine di attuare componenti SPA modificabili nell&#39;ambito dell&#39;AEM.

>[!NOTE]
>
>I seguenti requisiti sono indipendenti dal framework. Se questi requisiti sono soddisfatti, è possibile fornire un livello specifico del framework composto da moduli, componenti e servizi.
>
>**Questi requisiti sono già soddisfatti per i quadri di riferimento React e Angular nell’AEM.** I requisiti di questo blueprint sono pertinenti solo se desideri implementare un altro framework per l’utilizzo con AEM.

>[!CAUTION]
>
>Sebbene le capacità dell’AEM in materia di SPA siano indipendenti dal quadro, attualmente sono supportati solo i quadri React e Angular.

Per consentire all’autore di utilizzare l’Editor pagina AEM per modificare i dati esposti da un framework di applicazione a pagina singola, un progetto deve essere in grado di interpretare la struttura del modello che rappresenta la semantica dei dati memorizzati per un’applicazione all’interno dell’archivio AEM. Per raggiungere questo obiettivo, vengono fornite due librerie indipendenti dal framework: `PageModelManager` e `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

Il `PageModelManager` La libreria viene fornita come pacchetto NPM da utilizzare per un progetto SPA. Accompagna l&#39;SPA e funge da gestore del modello di dati.

Per conto dell’SPA, astrae il recupero e la gestione della struttura JSON che rappresenta l’effettiva struttura del contenuto. È anche responsabile della sincronizzazione con l&#39;SPA per comunicare quando deve rieseguire il rendering dei suoi componenti.

Vedere il pacchetto NPM [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

Quando si inizializza `PageModelManager`, la libreria carica innanzitutto il modello principale fornito dell’app (tramite il parametro, la proprietà meta o l’URL corrente). Se la libreria identifica che il modello della pagina corrente non fa parte del modello principale che recupera e lo include come modello di una pagina figlio.

![page_model_consolidation](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

Il `ComponentMapping` viene fornito come pacchetto NPM al progetto front-end. Memorizza i componenti front-end e consente all’SPA di mappare i componenti front-end ai tipi di risorse AEM. Ciò abilita una risoluzione dinamica dei componenti durante l’analisi del modello JSON dell’applicazione.

Ogni elemento presente nel modello contiene un `:type` che espone un tipo di risorsa AEM. Una volta montato, il componente front-end può eseguire il rendering utilizzando il frammento di modello ricevuto dalle librerie sottostanti.

#### Mappatura di un modello dinamico a un componente {#dynamic-model-to-component-mapping}

Per informazioni dettagliate su come avviene la mappatura del modello dinamico ai componenti nell’SDK per AEM di JavaScript per SPA, consulta l’articolo [Mappatura di un modello dinamico a un componente per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### Livello specifico del framework {#framework-specific-layer}

È necessario implementare un terzo livello per ogni framework front-end. Questa terza libreria è responsabile dell’interazione con le librerie sottostanti e fornisce una serie di punti di ingresso ben integrati e di facile utilizzo per l’interazione con il modello di dati.

Il resto del presente documento descrive i requisiti di questo livello specifico del quadro intermedio e aspira ad essere indipendente dal quadro. Nel rispetto dei seguenti requisiti, è possibile fornire un livello specifico per il framework affinché i componenti del progetto interagiscano con le librerie sottostanti incaricate di gestire il modello di dati.

## Concetti generali {#general-concepts}

### Modello pagina {#page-model}

La struttura del contenuto della pagina è memorizzata in AEM. Il modello della pagina viene utilizzato per mappare e creare istanze dei componenti SPA. Gli sviluppatori dell&#39;SPA creano i componenti dell&#39;SPA che mappano ai componenti dell&#39;AEM. A tal fine, utilizzano il tipo di risorsa (o il percorso del componente AEM) come chiave univoca.

I componenti SPA devono essere sincronizzati con il modello della pagina e devono essere aggiornati di conseguenza con qualsiasi modifica al relativo contenuto. Un pattern che sfrutta i componenti dinamici deve essere utilizzato per creare istantaneamente istanze di componenti seguendo la struttura del modello di pagina fornita.

### Meta campi {#meta-fields}

Il modello di pagina sfrutta JSON Model Exporter, che a sua volta è basato su [Modello Sling](https://sling.apache.org/documentation/bundles/models.html) API. I modelli sling esportabili espongono il seguente elenco di campi per consentire alle librerie sottostanti di interpretare il modello di dati:

* `:type`: tipo della risorsa AEM (predefinito = tipo di risorsa)
* `:children`: elementi figlio gerarchici della risorsa corrente. Gli elementi figlio non fanno parte del contenuto interno della risorsa corrente (sono disponibili negli elementi che rappresentano una pagina)
* `:hierarchyType`: tipo gerarchico di una risorsa. Il `PageModelManager` attualmente supporta il tipo di pagina

* `:items`: risorse di contenuto figlio della risorsa corrente (struttura nidificata, presente solo nei contenitori)
* `:itemsOrder`: elenco ordinato dei figli. L’oggetto mappa JSON non garantisce l’ordine dei relativi campi. Grazie alla mappa e all’array corrente, il consumatore dell’API beneficia di entrambe le strutture
* `:path`: percorso del contenuto di un elemento (presente negli elementi che rappresentano una pagina)

Vedi anche [Guida introduttiva di AEM Content Services.](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### Modulo specifico per framework {#framework-specific-module}

Separare i dubbi aiuta a facilitare l’implementazione del progetto. Pertanto, è necessario fornire un pacchetto specifico per npm. Questo pacchetto è responsabile dell’aggregazione e dell’esposizione dei moduli, dei servizi e dei componenti di base. Questi componenti devono incapsulare la logica di gestione del modello dati e fornire accesso ai dati previsti dal componente del progetto. Il modulo è anche responsabile dell’esposizione transitiva di utili punti di ingresso delle librerie sottostanti.

Per facilitare l’interoperabilità delle librerie, Adobe consiglia al modulo specifico per il framework di raggruppare le seguenti librerie. Se necessario, il livello può incapsulare e adattare le API sottostanti prima di esporle al progetto.

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

A questo scopo, il provider di modelli deve registrarsi nel ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. Quindi, quando si verifica una modifica, riceve e trasmette i dati aggiornati al componente delegato. Per convenzione, la proprietà resa disponibile al componente delegante che conterrà il frammento del modello è denominata `cqModel`. L’implementazione è libera di fornire questa proprietà al componente, ma deve considerare aspetti quali l’integrazione con l’architettura del framework, la possibilità di individuare e la facilità d’uso.

### Il componente HTML Decorator {#the-component-html-decorator}

Il Component Decorator è responsabile della decorazione delle HTML esterne dell’elemento di ogni istanza del componente con una serie di attributi di dati e nomi di classi previsti dall’Editor pagina.

#### Dichiarazione del componente {#component-declaration}

I metadati seguenti devono essere aggiunti all’elemento HTML esterno prodotto dal componente del progetto. Consentono all’Editor pagina di recuperare la configurazione di modifica corrispondente.

* `data-cq-data-path`: percorso della risorsa relativo al `jcr:content`

#### Modifica della dichiarazione di capacità e del segnaposto {#editing-capability-declaration-and-placeholder}

I metadati e i nomi di classi seguenti devono essere aggiunti all&#39;elemento HTML esterno prodotto dal componente del progetto. Consentono all’Editor pagina di offrire funzionalità correlate.

* `cq-placeholder`: nome della classe che identifica il segnaposto per un componente vuoto
* `data-emptytext`: etichetta che deve essere visualizzata dalla sovrapposizione quando un’istanza del componente è vuota

**Segnaposto per componenti vuoti**

Ogni componente deve essere esteso con una funzionalità che decorerà l’elemento HTML esterno con attributi di dati e nomi di classi specifici per segnaposto e sovrapposizioni correlate quando il componente viene identificato come vuoto.

**Informazioni sul valore Vuoto di un componente**

* Il componente è logicamente vuoto?
* Qual è l’etichetta visualizzata dalla sovrapposizione quando il componente è vuoto?

### Contenitore {#container}

Un contenitore è un componente destinato a contenere ed eseguire il rendering dei componenti figlio. A questo scopo, il contenitore scorre la `:itemsOrder`, `:items` e `:children` proprietà del relativo modello.

Il contenitore ottiene dinamicamente i componenti figlio dall’archivio della [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) libreria. Il contenitore estende quindi il componente secondario con le funzionalità del provider di modelli e infine lo crea come istanza.

### Pagina {#page}

Il `Page` il componente estende `Container` componente. Un contenitore è un componente destinato a contenere ed eseguire il rendering dei componenti figlio, incluse le pagine figlie. A questo scopo, il contenitore scorre la `:itemsOrder`, `:items`, e `:children` proprietà del relativo modello. Il `Page` componente ottiene dinamicamente i componenti figlio dall&#39;archivio del [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping) libreria. Il `Page` è responsabile della creazione di un&#39;istanza dei componenti figlio.

### Griglia dinamica {#responsive-grid}

Il componente Griglia reattiva è un contenitore. Contiene una variante specifica del provider di modelli che rappresenta le relative colonne. La griglia reattiva e le sue colonne sono responsabili della decorazione dell’elemento HTML esterno del componente del progetto con i nomi di classi specifici contenuti nel modello.

Il componente Griglia reattiva deve essere pre-mappato alla sua controparte AEM, in quanto è complesso e raramente personalizzato.

#### Campi modello specifici {#specific-model-fields}

* `gridClassNames:` Nomi di classe forniti per la griglia reattiva
* `columnClassNames:` Nomi di classe forniti per la colonna reattiva

#### Segnaposto della griglia reattiva {#placeholder-of-the-reponsive-grid}

Il componente SPA è mappato a un contenitore grafico come la griglia reattiva e deve aggiungere un segnaposto figlio virtuale durante la creazione del contenuto. Quando il contenuto dell’SPA viene creato dall’Editor pagina, viene incorporato nell’editor utilizzando un iframe e il `data-cq-editor` viene aggiunto al nodo del documento del contenuto. Quando `data-cq-editor` è presente, il contenitore deve includere un elemento HTMLElement per rappresentare l’area con cui l’autore interagisce quando inserisce un nuovo componente nella pagina.

Ad esempio:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>I nomi delle classi utilizzati nell’esempio sono attualmente richiesti dall’editor di pagine.
>
>* `"new section"`: indica che l’elemento corrente è il segnaposto del contenitore
>* `"aem-Grid-newComponent"`: normalizza il componente per la creazione del layout
>


#### Mappatura dei componenti {#component-mapping}

Il sottostante [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) libreria e relativi `MapTo` Questa funzione può essere incapsulata ed estesa per fornire le funzionalità relative alla configurazione di modifica fornita insieme alla classe del componente corrente.

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

Nell’implementazione di cui sopra, il componente del progetto viene esteso con la funzionalità di vuoto prima che il venga effettivamente registrato nel [Mappatura dei componenti](/help/sites-developing/spa-blueprint.md#componentmapping) archiviare. Ciò avviene incapsulando ed estendendo il [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) per introdurre il supporto della funzionalità `EditConfig` oggetto di configurazione:

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

* L’elemento griglia reattivo contiene nomi di classi con prefisso `aem-Grid--`
* L’elemento della colonna reattivo presenta nomi di classi con prefisso `aem-GridColumn--`
* Viene racchiusa una griglia reattiva che è anche la colonna di una griglia padre, ad esempio i due prefissi precedenti non vengono visualizzati sullo stesso elemento
* Gli elementi corrispondenti alle risorse modificabili includono `data-cq-data-path` proprietà. Consulta la [Contrarre con l’Editor pagina](#contract-wtih-the-page-editor) sezione del presente documento.

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

Il sottostante [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) libreria e relativi ` [ModelRouter](/help/sites-developing/spa-routing.md)` Il modulo (abilitato per impostazione predefinita) è responsabile della preacquisizione e dell’accesso al modello associato a un determinato percorso di risorsa.

Le due entità si riferiscono alla nozione di ciclo, ma ` [ModelRouter](/help/sites-developing/spa-routing.md)` è responsabile solo dell&#39;esecuzione ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` caricato con un modello dati strutturato in sincronia con lo stato corrente dell’applicazione.

Vedi l’articolo [Routing modello SPA](/help/sites-developing/spa-routing.md) per ulteriori informazioni.

## SPA in azione {#spa-in-action}

Scopri come funziona un semplice SPA e come sperimentare autonomamente un SPA continuando a consultare il documento [Guida introduttiva dell’SPA nell’AEM](/help/sites-developing/spa-getting-started-react.md).

## Ulteriori informazioni {#further-reading}

Per maggiori informazioni sull’SPA nell’AEM, consulta i seguenti documenti:

* [Panoramica sull’authoring di SPA](/help/sites-developing/spa-overview.md) per una panoramica dell&#39;SPA nell&#39;AEM e del modello di comunicazione
* [Guida introduttiva dell’SPA nell’AEM](/help/sites-developing/spa-getting-started-react.md) per una guida ad un SPA semplice e come funziona
