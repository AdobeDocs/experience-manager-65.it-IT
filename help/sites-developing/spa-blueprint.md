---
title: Blueprint SPA
seo-title: Blueprint SPA
description: Il presente documento descrive il contratto generale, indipendente dal quadro, che ogni quadro SPA dovrebbe rispettare per implementare componenti SPA modificabili all'interno di AEM.
seo-description: Il presente documento descrive il contratto generale, indipendente dal quadro, che ogni quadro SPA dovrebbe rispettare per implementare componenti SPA modificabili all'interno di AEM.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 0%

---


# SPA Blueprint{#spa-blueprint}

Per consentire all’autore di utilizzare l’editor SPA AEM per modificare il contenuto di un SPA, il SPA deve soddisfare alcuni requisiti descritti in questo documento.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad es. React o Angular).

## Introduzione {#introduction}

Il presente documento descrive il contratto generale che ogni framework SPA deve soddisfare (ossia il tipo di livello di supporto AEM) per implementare componenti SPA modificabili all&#39;interno di AEM.

>[!NOTE]
>
>I seguenti requisiti sono indipendenti dal framework. Se questi requisiti sono soddisfatti, è possibile fornire uno strato specifico del framework composto da moduli, componenti e servizi.
>
>**Tali requisiti sono già soddisfatti per i quadri React e Angular in AEM.** I requisiti di questo modello sono rilevanti solo se desiderate implementare un altro framework da utilizzare con AEM.

>[!CAUTION]
>
>Sebbene le capacità SPA di AEM siano indipendenti dal framework, al momento sono supportati solo i framework React e Angular.

Per consentire all&#39;autore di utilizzare l&#39;Editor pagina AEM per modificare i dati esposti da un framework Applicazione pagina singola, un progetto deve essere in grado di interpretare la struttura del modello che rappresenta la semantica dei dati memorizzati per un&#39;applicazione all&#39;interno dell&#39;archivio AEM. Per raggiungere questo obiettivo, vengono fornite due librerie non basate sul framework: `PageModelManager` e `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

La libreria `PageModelManager` viene fornita come pacchetto NPM da utilizzare in un progetto SPA. Associa il SPA e funge da gestore di modelli di dati.

Per conto del SPA, l&#39;articolo illustra il recupero e la gestione della struttura JSON che rappresenta la struttura di contenuto effettiva. È inoltre responsabile della sincronizzazione con il SPA per informarlo quando deve eseguire nuovamente il rendering dei suoi componenti.

Vedere il pacchetto NPM [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

Quando si inizializza la `PageModelManager`, la libreria carica innanzitutto il modello principale fornito per l&#39;app (tramite parametro, proprietà meta o URL corrente). Se la libreria identifica che il modello della pagina corrente non fa parte del modello principale, recupera e lo include come modello di una pagina figlia.

![page_model_Consolidation](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

Il modulo `ComponentMapping` viene fornito come pacchetto NPM al progetto front-end. memorizza i componenti front-end e consente al SPA di mappare i componenti front-end sui tipi di risorse AEM. Questo consente una risoluzione dinamica dei componenti durante l&#39;analisi del modello JSON dell&#39;applicazione.

Ogni elemento presente nel modello contiene un campo `:type` che espone un tipo di risorsa AEM. Quando è montato, il componente front-end può eseguire il rendering utilizzando il frammento del modello ricevuto dalle librerie sottostanti.

#### Mappatura modello dinamico a componente {#dynamic-model-to-component-mapping}

Per informazioni dettagliate su come si verifica la mappatura del modello dinamico al componente nell’SDK SPA JavaScript per AEM consultate l’articolo [Mappatura del modello dinamico al componente per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### Livello specifico del framework {#framework-specific-layer}

Per ogni struttura front-end deve essere implementato un terzo livello. Questa terza libreria è responsabile dell&#39;interazione con le librerie sottostanti e fornisce una serie di punti di ingresso integrati e di facile utilizzo per l&#39;interazione con il modello dati.

Il resto del presente documento descrive i requisiti di questo livello specifico del quadro intermedio e aspira ad essere indipendente dal framework. Rispettando i seguenti requisiti, è possibile fornire ai componenti del progetto un livello specifico per il framework che consenta loro di interagire con le librerie sottostanti responsabili della gestione del modello dati.

## Concetti generali {#general-concepts}

### Modello pagina {#page-model}

La struttura del contenuto della pagina viene memorizzata in AEM. Il modello della pagina viene utilizzato per mappare e creare SPA componenti. Gli sviluppatori SPA creano SPA componenti che vengono mappati su AEM componenti. A tal fine, utilizzano il tipo di risorsa (o percorso del componente AEM) come chiave univoca.

I componenti SPA devono essere sincronizzati con il modello di pagina ed essere aggiornati di conseguenza con eventuali modifiche al contenuto. È necessario utilizzare un pattern che sfrutta componenti dinamici per creare al volo le istanze dei componenti seguendo la struttura del modello di pagina fornita.

### Campi metadati {#meta-fields}

Il modello di pagina sfrutta l&#39;Esportatore di modelli JSON, anch&#39;esso basato sull&#39;API [Sling Model](https://sling.apache.org/documentation/bundles/models.html). I modelli di sling esportabili mostrano il seguente elenco di campi per consentire alle librerie sottostanti di interpretare il modello di dati:

* `:type`: Tipo della risorsa AEM (predefinito = tipo di risorsa)
* `:children`: Elementi secondari gerarchici della risorsa corrente. Gli elementi figlio non fanno parte del contenuto interno della risorsa corrente (si trova sugli elementi che rappresentano una pagina)
* `:hierarchyType`: Tipo gerarchico di una risorsa. Il `PageModelManager` supporta attualmente il tipo di pagina

* `:items`: Risorse di contenuto figlio della risorsa corrente (struttura nidificata, presenti solo in contenitori)
* `:itemsOrder`: Elenco ordinato degli elementi figlio. L&#39;oggetto mappa JSON non garantisce l&#39;ordine dei relativi campi. Avendo sia la mappa che l&#39;array corrente, il consumatore dell&#39;API ha i vantaggi di entrambe le strutture
* `:path`: Percorso del contenuto di un elemento (presente su elementi che rappresentano una pagina)

Vedere anche [Guida introduttiva a AEM Content Services.](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### Modulo specifico per il framework {#framework-specific-module}

Separare i problemi aiuta a facilitare l&#39;implementazione del progetto. Occorre pertanto fornire un pacchetto specifico per il npm. Questo pacchetto è responsabile dell&#39;aggregazione e dell&#39;esposizione dei moduli di base, dei servizi e dei componenti. Questi componenti devono racchiudere la logica di gestione del modello dati e fornire l&#39;accesso ai dati previsti dal componente del progetto. Il modulo è inoltre responsabile dell&#39;esposizione transitiva dei punti di ingresso utili delle librerie sottostanti.

Per facilitare l&#39;interoperabilità delle librerie,  Adobe consiglia al modulo specifico del quadro di creare i pacchetti delle seguenti librerie. Se necessario, il livello può racchiudere e adattare le API sottostanti prima di esporle al progetto.

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### Implementazioni {#implementations}

#### Reagisce {#react}

modulo npm: [@adobe/aem-response-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angolare {#angular}

modulo npm: presto

## Servizi principali e componenti {#main-services-and-components}

Le seguenti entità dovrebbero essere attuate conformemente agli orientamenti specifici di ciascun quadro. In base all&#39;architettura del quadro, l&#39;implementazione può variare notevolmente, ma devono essere fornite le funzionalità descritte.

### Provider di modelli {#the-model-provider}

I componenti di progetto devono delegare l&#39;accesso ai frammenti di un modello a un provider di modelli. Il provider del modello è quindi incaricato di ascoltare le modifiche apportate al frammento specificato del modello e di restituire il modello aggiornato al componente delegante.

A tal fine, il provider del modello deve registrarsi nel percorso ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. Quando si verifica una modifica, riceve e trasmette i dati aggiornati al componente delegante. Per convenzione, la proprietà messa a disposizione del componente delegante che porterà il frammento del modello è denominata `cqModel`. L&#39;implementazione è libera di fornire questa proprietà al componente, ma dovrebbe considerare aspetti quali l&#39;integrazione con l&#39;architettura del framework, la possibilità di scoprire e la facilità d&#39;uso.

### Il decoratore HTML del componente {#the-component-html-decorator}

Il decoratore dei componenti è responsabile della decorazione dell’HTML esterno dell’elemento di ogni istanza di componente con una serie di attributi di dati e nomi di classe previsti dall’Editor pagina.

#### Dichiarazione componente {#component-declaration}

I seguenti metadati devono essere aggiunti all&#39;elemento HTML esterno prodotto dal componente del progetto. Consentono all’Editor pagina di recuperare la configurazione di modifica corrispondente.

* `data-cq-data-path`: Percorso della risorsa relativa al  `jcr:content`

#### Dichiarazione di funzionalità di modifica e segnaposto {#editing-capability-declaration-and-placeholder}

I seguenti metadati e nomi di classe devono essere aggiunti all&#39;elemento HTML esterno prodotto dal componente del progetto. Consentono all’Editor pagina di offrire funzionalità correlate.

* `cq-placeholder`: Nome della classe che identifica il segnaposto per un componente vuoto
* `data-emptytext`: Etichetta visualizzata dalla sovrapposizione quando un’istanza di componente è vuota

**Segnaposto per componenti vuoti**

Ogni componente deve essere esteso con una funzionalità che decori l’elemento HTML esterno con attributi di dati e nomi di classe specifici per i segnaposto e le sovrapposizioni correlate quando il componente è identificato come vuoto.

**Informazioni sul vuoto di un componente**

* Il componente è logicamente vuoto?
* Che etichetta deve essere visualizzata dalla sovrapposizione quando il componente è vuoto?

### Contenitore {#container}

Un contenitore è un componente destinato a contenere ed eseguire il rendering di componenti secondari. A tal fine, il contenitore esegue un&#39;iterazione sulle proprietà `:itemsOrder`, `:items` e `:children` del proprio modello.

Il contenitore ottiene in modo dinamico i componenti secondari dallo store della libreria ` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)`. Il contenitore quindi estende il componente secondario con le funzionalità del provider di modelli e, infine, lo crea come istanza.

### Pagina {#page}

Il componente `Page` estende il componente `Container`. Un contenitore è un componente destinato a contenere ed eseguire il rendering dei componenti secondari, incluse le pagine figlie. A tal fine, il contenitore esegue un&#39;iterazione sulle proprietà `:itemsOrder`, `:items` e `:children` del modello. Il componente `Page` ottiene dinamicamente i componenti secondari dallo store della libreria [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping). `Page` è responsabile della creazione di istanze di componenti secondari.

### Griglia reattiva {#responsive-grid}

Il componente Griglia reattiva è un contenitore. Contiene una variante specifica del provider di modelli che ne rappresenta le colonne. La griglia reattiva e le relative colonne sono responsabili della decorazione dell’elemento HTML esterno del componente del progetto con i nomi di classe specifici contenuti nel modello.

Il componente Griglia reattiva deve essere pre-mappato sulla sua controparte AEM poiché è complesso e raramente personalizzato.

#### Campi modello specifici {#specific-model-fields}

* `gridClassNames:` Nomi di classe forniti per la griglia reattiva
* `columnClassNames:` Nomi di classe forniti per la colonna reattiva

Consultate anche la risorsa npm [@adobe/aem-response-editable-components#srccomponentsresponsivegridjsx](https://www.npmjs.com/package/@adobe/aem-react-editable-components#srccomponentsresponsivegridjsx)

#### Segnaposto della griglia di risposta {#placeholder-of-the-reponsive-grid}

Il componente SPA è mappato a un contenitore grafico, ad esempio la griglia reattiva, e deve aggiungere un segnaposto virtuale secondario al momento della creazione del contenuto. Quando il contenuto del SPA viene creato dall&#39;Editor pagina, tale contenuto viene incorporato nell&#39;editor utilizzando un iframe e l&#39;attributo `data-cq-editor` viene aggiunto al nodo del documento di tale contenuto. Quando l&#39;attributo `data-cq-editor` è presente, il contenitore deve includere un oggetto HTMLElement per rappresentare l&#39;area con la quale l&#39;autore interagisce quando inserisce un nuovo componente nella pagina.

Esempio:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>I nomi delle classi utilizzati nell&#39;esempio sono attualmente richiesti dall&#39;editor pagina.
>
>* `"new section"`: Indica che l&#39;elemento corrente è il segnaposto del contenitore
>* `"aem-Grid-newComponent"`: Normalizza il componente per l’authoring dei layout

>



#### Mapping componente {#component-mapping}

La [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) libreria sottostante e la relativa funzione `MapTo` possono essere racchiusi ed estesi per fornire le funzionalità relative alla configurazione di modifica fornita insieme alla classe di componenti corrente.

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

Nell&#39;implementazione precedente, il componente del progetto viene esteso con la funzionalità di svuotamento prima che venga effettivamente registrato nello store [Mappatura componente](/help/sites-developing/spa-blueprint.md#componentmapping). A tal fine, è possibile incorporare ed estendere la libreria [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) per introdurre il supporto dell&#39;oggetto di configurazione `EditConfig`:

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

## Contratto con Editor pagina {#contract-with-the-page-editor}

I componenti del progetto devono generare almeno i seguenti attributi di dati per consentire all’editor di interagire con essi.

* `data-cq-data-path`: Percorso relativo del componente, come fornito da  `PageModel` (ad esempio,  `"root/responsivegrid/image"`). Questo attributo non deve essere aggiunto alle pagine.

In sintesi, per essere interpretato dall’editor pagina come modificabile, un componente di progetto deve rispettare il seguente contratto:

* Fornire gli attributi previsti per associare un’istanza di componente front-end a una risorsa AEM.
* Fornire la serie prevista di attributi e nomi di classe che consente la creazione di segnaposto vuoti.
* Fornite i nomi di classe previsti per il trascinamento delle risorse.

### Struttura tipica degli elementi HTML {#typical-html-element-structure}

Il frammento seguente illustra la tipica rappresentazione HTML di una struttura di contenuto di pagina. Ecco alcuni punti importanti:

* L&#39;elemento griglia reattiva contiene i nomi delle classi con il prefisso `aem-Grid--`
* L&#39;elemento colonna reattivo contiene nomi di classe con il prefisso `aem-GridColumn--`
* Viene racchiusa una griglia reattiva che è anche la colonna di una griglia padre, in modo che i due prefissi precedenti non vengano visualizzati sullo stesso elemento
* Gli elementi corrispondenti alle risorse modificabili contengono una proprietà `data-cq-data-path`. Vedere la sezione [Contratto con l&#39;Editor pagina](#contract-wtih-the-page-editor) di questo documento.

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

## Navigazione e routing {#navigation-and-routing}

L&#39;app è proprietaria del routing. Lo sviluppatore front-end deve innanzitutto implementare un componente Navigazione (mappato su un componente di navigazione AEM). Questo componente eseguirebbe il rendering dei collegamenti URL da utilizzare insieme a una serie di route per visualizzare o nascondere frammenti di contenuto.

La [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) libreria sottostante e il relativo modulo ` [ModelRouter](/help/sites-developing/spa-routing.md)` (attivato per impostazione predefinita) sono responsabili della preacquisizione e dell&#39;accesso al modello associato a un determinato percorso di risorse.

Le due entità si riferiscono al concetto di routing, ma la ` [ModelRouter](/help/sites-developing/spa-routing.md)` è responsabile solo del caricamento della ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` con un modello dati strutturato in sincronia con lo stato dell&#39;applicazione corrente.

Per ulteriori informazioni, vedere l&#39;articolo [SPA modello di routing](/help/sites-developing/spa-routing.md).

## SPA in azione {#spa-in-action}

Scopri come un semplice SPA funziona e sperimenta con un SPA personale continuando con il documento [Guida introduttiva a SPA in AEM](/help/sites-developing/spa-getting-started-react.md).

## Lettura successiva {#further-reading}

Per ulteriori informazioni sulle SPA in AEM, consulta i documenti seguenti:

* [SPA ](/help/sites-developing/spa-overview.md) Panoramica sull’authoring per una panoramica delle SPA in AEM e del modello di comunicazione
* [Guida introduttiva alle SPA in ](/help/sites-developing/spa-getting-started-react.md) AEM per una guida a un semplice SPA e al funzionamento
