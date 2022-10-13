---
title: Blueprint SPA
seo-title: SPA Blueprint
description: Il presente documento descrive il contratto generale, indipendente dal quadro, che ogni quadro SPA dovrebbe rispettare per implementare componenti SPA modificabili all'interno di AEM.
seo-description: This document describes the general, framework-independent contract that any SPA framework should fulfill in order to implement editable SPA components within AEM.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
source-git-commit: e13953bed73481738832a00a7563a07149c2d3bd
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 1%

---

# Blueprint SPA{#spa-blueprint}

Per consentire all’autore di utilizzare l’editor di SPA AEM per modificare il contenuto di un SPA, sono necessari requisiti che l’SPA deve soddisfare, descritti in questo documento.

>[!NOTE]
>
>L’editor di SPA è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad esempio, React o Angular).

## Introduzione {#introduction}

Il presente documento descrive il contratto generale che ogni quadro SPA deve rispettare (cioè il tipo di livello di supporto AEM) per implementare componenti SPA modificabili all&#39;interno di AEM.

>[!NOTE]
>
>I seguenti requisiti sono indipendenti dal framework. Se questi requisiti sono soddisfatti, è possibile fornire un livello specifico del framework composto da moduli, componenti e servizi.
>
>**Questi requisiti sono già soddisfatti per i framework React e Angular in AEM.** I requisiti di questo modello sono rilevanti solo se desideri implementare un altro framework da utilizzare con AEM.

>[!CAUTION]
>
>Sebbene le funzionalità SPA di AEM siano indipendenti dal framework, al momento sono supportati solo i framework React e Angular.

Per consentire all’autore di utilizzare l’Editor pagina AEM per modificare i dati esposti da un framework di applicazione a pagina singola, un progetto deve essere in grado di interpretare la struttura del modello che rappresenta la semantica dei dati memorizzati per un’applicazione all’interno dell’archivio AEM. Per raggiungere questo obiettivo, vengono fornite due librerie agnostiche del framework: la `PageModelManager` e `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

La `PageModelManager` La libreria viene fornita come pacchetto NPM da utilizzare in un progetto SPA. Associa il SPA e funge da responsabile del modello dati.

Per conto della SPA, astratta il recupero e la gestione della struttura JSON che rappresenta la struttura del contenuto effettiva. È anche responsabile della sincronizzazione con il SPA per informarlo quando deve eseguire nuovamente il rendering dei suoi componenti.

Vedi il pacchetto NPM [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

Inizializzazione di `PageModelManager`, la libreria carica prima il modello principale fornito dell’app (tramite parametro , proprietà meta o URL corrente). Se la libreria rileva che il modello della pagina corrente non fa parte del modello principale, lo recupera e lo include come modello di una pagina figlio.

![page_model_consolidamento](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

La `ComponentMapping` Il modulo viene fornito come pacchetto NPM al progetto front-end. Memorizza i componenti front-end e consente al SPA di mappare i componenti front-end sui tipi di risorse AEM. In questo modo si abilita una risoluzione dinamica dei componenti durante l’analisi del modello JSON dell’applicazione.

Ogni elemento presente nel modello contiene un `:type` campo che espone un tipo di risorsa AEM. Quando è montato, il componente front-end può renderizzarsi utilizzando il frammento di modello ricevuto dalle librerie sottostanti.

#### Mappatura di un modello dinamico a un componente {#dynamic-model-to-component-mapping}

Per informazioni dettagliate su come si verifica la mappatura del modello dinamico ai componenti nell’SDK SPA JavaScript per AEM consulta l’articolo [Mappatura dinamica da modello a componente per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### Livello specifico del framework {#framework-specific-layer}

Deve essere implementato un terzo livello per ogni framework front-end. Questa terza libreria è responsabile dell’interazione con le librerie sottostanti e fornisce una serie di punti di ingresso ben integrati e facili da usare per l’interazione con il modello dati.

Il resto del presente documento descrive i requisiti di questo livello specifico del quadro intermedio e aspira ad essere indipendente dal quadro. Rispettando i seguenti requisiti, è possibile fornire un livello specifico per il framework affinché i componenti del progetto interagiscano con le librerie sottostanti al fine di gestire il modello dati.

## Concetti generali {#general-concepts}

### Modello a pagina {#page-model}

La struttura del contenuto della pagina viene memorizzata in AEM. Il modello della pagina viene utilizzato per mappare e creare un’istanza SPA componenti. Gli sviluppatori SPA creano SPA componenti che mappano a componenti AEM. A questo scopo, utilizzano il tipo di risorsa (o il percorso del componente AEM) come chiave univoca.

I componenti SPA devono essere sincronizzati con il modello di pagina e devono essere aggiornati con eventuali modifiche al contenuto. È necessario utilizzare un pattern che sfrutta i componenti dinamici per creare al volo le istanze dei componenti seguendo la struttura del modello di pagina fornita.

### Metadati {#meta-fields}

Il modello di pagina sfrutta l’esportazione del modello JSON, anch’esso basato su [Modello Sling](https://sling.apache.org/documentation/bundles/models.html) API. I modelli sling esportabili espongono il seguente elenco di campi per consentire alle librerie sottostanti di interpretare il modello dati:

* `:type`: Tipo della risorsa AEM (predefinito = tipo di risorsa)
* `:children`: Elementi secondari gerarchici della risorsa corrente. Gli elementi figlio non fanno parte del contenuto interno della risorsa corrente (si trova sugli elementi che rappresentano una pagina)
* `:hierarchyType`: Tipo gerarchico di una risorsa. La `PageModelManager` attualmente supporta il tipo di pagina

* `:items`: Risorse di contenuto figlio della risorsa corrente (struttura nidificata, presente solo nei contenitori)
* `:itemsOrder`: Elenco ordinato dei figli. L&#39;oggetto mappa JSON non garantisce l&#39;ordine dei campi. Avendo sia la mappa che l’array corrente, il consumatore dell’API ha i vantaggi di entrambe le strutture
* `:path`: Percorso del contenuto di un elemento (presente in elementi che rappresentano una pagina)

Vedi anche [Guida introduttiva a AEM Content Services.](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### Modulo specifico per il framework {#framework-specific-module}

La separazione dei problemi aiuta ad agevolare l&#39;implementazione dei progetti. È pertanto opportuno fornire un pacchetto specifico per il npm. Questo pacchetto è responsabile dell&#39;aggregazione e dell&#39;esposizione dei moduli, servizi e componenti di base. Questi componenti devono incapsulare la logica di gestione del modello dati e fornire l’accesso ai dati attesi dal componente del progetto. Il modulo è inoltre responsabile dell’esposizione transitoria di punti di ingresso utili delle librerie sottostanti.

Per facilitare l&#39;interoperabilità delle librerie, l&#39;Adobe consiglia al modulo specifico del framework di raggruppare le seguenti librerie. Se necessario, il livello può incapsulare e adattare le API sottostanti prima di esporle al progetto.

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### Implementazioni {#implementations}

#### Reagire {#react}

modulo npm: [@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

modulo npm: [@adobe/aem-angular-editable-components](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## Servizi e componenti principali {#main-services-and-components}

Le seguenti entità devono essere attuate conformemente agli orientamenti specifici di ciascun quadro di riferimento. In base all’architettura del framework, l’implementazione può variare notevolmente, ma devono essere fornite le funzionalità descritte.

### Provider di modelli {#the-model-provider}

I componenti di progetto devono delegare l&#39;accesso ai frammenti di un modello a un provider di modelli. Il Model Provider è quindi incaricato di ascoltare le modifiche apportate al frammento specificato del modello e di restituire il modello aggiornato al componente delegante.

A questo scopo, il provider di modelli deve registrarsi nel ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. Quindi, quando si verifica una modifica, riceve e trasmette i dati aggiornati al componente delegante. Per convenzione, la proprietà resa disponibile al componente delegante che trasporterà il frammento del modello viene denominata `cqModel`. L’implementazione è libera di fornire questa proprietà al componente, ma dovrebbe considerare aspetti quali l’integrazione con l’architettura del framework, la possibilità di individuare e la facilità d’uso.

### Component HTML Decorator {#the-component-html-decorator}

Il decoratore componente è responsabile della decorazione del HTML esterno dell’elemento di ciascuna istanza di componente con una serie di attributi di dati e nomi di classe previsti dall’Editor pagina.

#### Dichiarazione del componente {#component-declaration}

I seguenti metadati devono essere aggiunti all’elemento HTML esterno prodotto dal componente del progetto. Consentono all’Editor pagina di recuperare la configurazione di modifica corrispondente.

* `data-cq-data-path`: Percorso della risorsa relativo al `jcr:content`

#### Dichiarazione e segnaposto della capacità di modifica {#editing-capability-declaration-and-placeholder}

I seguenti metadati e nomi di classe devono essere aggiunti all’elemento HTML esterno prodotto dal componente del progetto. Consentono all’Editor pagina di offrire funzionalità correlate.

* `cq-placeholder`: Nome della classe che identifica il segnaposto per un componente vuoto
* `data-emptytext`: Etichetta da visualizzare dalla sovrapposizione quando un’istanza di un componente è vuota

**Segnaposto per componenti vuoti**

Ogni componente deve essere esteso con una funzionalità che decori l’elemento HTML esterno con attributi di dati e nomi di classe specifici per i segnaposto e le sovrapposizioni correlate quando il componente è identificato come vuoto.

**Svuotamento di un componente**

* Il componente è logicamente vuoto?
* Qual è l’etichetta visualizzata dalla sovrapposizione quando il componente è vuoto?

### Contenitore {#container}

Un contenitore è un componente destinato a contenere ed eseguire il rendering dei componenti secondari. A tal fine, il contenitore si ripeterà sul `:itemsOrder`, `:items` e `:children` proprietà del modello.

Il contenitore ottiene in modo dinamico i componenti secondari dall’archivio del ` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)` libreria. Il contenitore estende quindi il componente secondario con le funzionalità del provider di modelli e, infine, lo crea in istanza.

### Pagina {#page}

La `Page` estensione del componente `Container` componente. Un contenitore è un componente destinato a contenere ed eseguire il rendering dei componenti secondari, incluse le pagine figlie. A tal fine, il contenitore si ripeterà sul `:itemsOrder`, `:items`e `:children` proprietà del modello. La `Page` il componente ottiene in modo dinamico i componenti secondari dall’archivio del [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping) libreria. La `Page` è responsabile della creazione di istanze dei componenti figlio.

### Griglia reattiva {#responsive-grid}

Il componente Griglia reattiva è un contenitore . Contiene una variante specifica del provider di modelli che rappresenta le sue colonne. La griglia reattiva e le sue colonne sono responsabili della decorazione dell’elemento HTML esterno del componente del progetto con i nomi di classe specifici contenuti nel modello.

Il componente Griglia reattiva deve essere pre-mappato sulla sua controparte AEM in quanto è complesso e raramente personalizzato.

#### Campi modello specifici {#specific-model-fields}

* `gridClassNames:` Nomi di classe forniti per la griglia reattiva
* `columnClassNames:` Nomi di classe forniti per la colonna reattiva

#### Segnaposto della griglia reattiva {#placeholder-of-the-reponsive-grid}

Il componente SPA è mappato a un contenitore grafico come la griglia reattiva e deve aggiungere un segnaposto figlio virtuale durante la creazione del contenuto. Quando il contenuto del SPA viene creato dall’Editor pagina, tale contenuto viene incorporato nell’editor utilizzando un iframe e il `data-cq-editor` viene aggiunto al nodo del documento di tale contenuto. Quando il `data-cq-editor` Il contenitore deve includere un elemento HTMLElement per rappresentare l&#39;area con cui l&#39;autore interagisce quando inserisce un nuovo componente nella pagina.

Esempio:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>I nomi delle classi utilizzati nell’esempio sono attualmente richiesti dall’editor pagina.
>
>* `"new section"`: Indica che l’elemento corrente è il segnaposto del contenitore
>* `"aem-Grid-newComponent"`: Normalizza il componente per la creazione del layout
>


#### Mappatura dei componenti {#component-mapping}

Il sottostante [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) la libreria e i relativi `MapTo` può essere incapsulata ed estesa per fornire le funzionalità relative alla configurazione di modifica fornita insieme alla classe di componente corrente.

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

Nell’implementazione precedente, il componente del progetto viene esteso con la funzionalità di vuoto prima che venga effettivamente registrato nel [Mappatura dei componenti](/help/sites-developing/spa-blueprint.md#componentmapping) archiviare. Questo viene fatto racchiudendo ed estendendo il [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) per introdurre il supporto del `EditConfig` oggetto di configurazione:

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

## Contratto con l’Editor pagina {#contract-with-the-page-editor}

I componenti del progetto devono generare almeno i seguenti attributi di dati per consentire all’editor di interagire con essi.

* `data-cq-data-path`: Percorso relativo del componente, come fornito dalla `PageModel` (ad esempio, `"root/responsivegrid/image"`). Questo attributo non deve essere aggiunto alle pagine.

In sintesi, per essere interpretato dall’editor di pagine come modificabile, un componente di progetto deve rispettare il contratto seguente:

* Fornisci gli attributi previsti per associare un’istanza di un componente front-end a una risorsa AEM.
* Fornire la serie prevista di attributi e nomi di classe che consente la creazione di segnaposto vuoti.
* Specifica i nomi di classe previsti per il trascinamento delle risorse.

### Struttura tipica degli elementi di HTML {#typical-html-element-structure}

Il frammento seguente illustra la tipica rappresentazione HTML di una struttura del contenuto di una pagina. Ecco alcuni punti importanti:

* L’elemento della griglia reattiva contiene i nomi delle classi con il prefisso `aem-Grid--`
* L’elemento della colonna dinamica contiene nomi di classe con prefisso `aem-GridColumn--`
* Una griglia reattiva, che è anche la colonna di una griglia padre, viene racchiusa, in modo che i due prefissi precedenti non vengano visualizzati sullo stesso elemento
* Gli elementi corrispondenti alle risorse modificabili hanno un `data-cq-data-path` proprietà. Consulta la sezione [Contratto con l’Editor pagina](#contract-wtih-the-page-editor) sezione di questo documento.

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

## Navigazione e instradamento {#navigation-and-routing}

L’app è proprietaria del routing. Lo sviluppatore front-end deve innanzitutto implementare un componente Navigazione (mappato a un componente di navigazione AEM). Questo componente esegue il rendering dei collegamenti URL da utilizzare insieme a una serie di percorsi che visualizzano o nascondono frammenti di contenuto.

Il sottostante [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) la libreria e i relativi ` [ModelRouter](/help/sites-developing/spa-routing.md)` Il modulo (abilitato per impostazione predefinita) è responsabile della preacquisizione e dell’accesso al modello associato a un determinato percorso di risorsa.

Le due entità si riferiscono alla nozione di indirizzamento ma ` [ModelRouter](/help/sites-developing/spa-routing.md)` è responsabile solo del ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` caricato con un modello dati strutturato in sincronia con lo stato dell&#39;applicazione corrente.

Vedi l&#39;articolo [Indirizzamento modello SPA](/help/sites-developing/spa-routing.md) per ulteriori informazioni.

## SPA in azione {#spa-in-action}

Scopri come funziona un semplice SPA e sperimentare un SPA da solo continuando sul documento [Guida introduttiva a SPA in AEM](/help/sites-developing/spa-getting-started-react.md).

## Ulteriori informazioni {#further-reading}

Per ulteriori informazioni sulle SPA in AEM, consulta i seguenti documenti:

* [Panoramica sull’authoring SPA](/help/sites-developing/spa-overview.md) per una panoramica del SPA in AEM e del modello di comunicazione
* [Guida introduttiva a SPA in AEM](/help/sites-developing/spa-getting-started-react.md) per una guida a un semplice SPA e come funziona
