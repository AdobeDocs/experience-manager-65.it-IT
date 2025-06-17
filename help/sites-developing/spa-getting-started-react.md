---
title: Guida introduttiva alle applicazioni a pagina singola in AEM - React
description: Questo articolo presenta un esempio di applicazione SPA, spiega come viene creata e come iniziare subito a utilizzare un’applicazione SPA personale con il framework React.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 4%

---


# Guida introduttiva alle applicazioni a pagina singola in AEM - React{#getting-started-with-spas-in-aem-react}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando framework SPA e gli autori desiderano modificare facilmente i contenuti all’interno di AEM per un sito creato utilizzando framework SPA.

La funzione di authoring di applicazioni a pagina singola offre una soluzione completa per il supporto di applicazioni a pagina singola in AEM. Questo articolo presenta un’applicazione SPA semplificata sul framework React, spiega come viene creata e come iniziare subito a utilizzare un’applicazione SPA personale.

>[!NOTE]
>
>Questo articolo si basa sul framework React. Per il documento corrispondente per il framework Angular, vedi [Guida introduttiva alle applicazioni a pagina singola in AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

{{ue-over-spa}}

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di una semplice applicazione a pagina singola e il minimo che è necessario sapere per eseguire l’operazione.

Per ulteriori dettagli sul funzionamento delle applicazioni a pagina singola in AEM, consulta i seguenti documenti:

* [Introduzione alla SPA e procedura dettagliata](/help/sites-developing/spa-walkthrough.md)
* [Introduzione all’authoring di applicazioni a pagina singola](/help/sites-developing/spa-overview.md)
* [Blueprint SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un’applicazione a pagina singola, i contenuti devono essere memorizzati in AEM ed essere esposti dal modello di contenuto.
>
>Un’applicazione a pagina singola sviluppata al di fuori di AEM non sarà autorizzabile se non rispetta il contratto del modello di contenuto.

Questo documento illustra la struttura di un’applicazione a pagina singola semplificata creata con il framework React e il suo funzionamento, consentendoti di applicare questa conoscenza all’applicazione a pagina singola.

## Dipendenze, configurazione e generazione {#dependencies-configuration-and-building}

Oltre alla prevista dipendenza da React, l’applicazione a pagina singola di esempio può utilizzare librerie aggiuntive per rendere più efficiente la creazione dell’applicazione a pagina singola.

### Dipendenze {#dependencies}

Il file `package.json` definisce i requisiti del pacchetto SPA complessivo. Le dipendenze minime di AEM per un’applicazione a pagina singola funzionante sono elencate qui.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Poiché questo esempio si basa sul framework React, nel file `package.json` sono obbligatorie due dipendenze specifiche di React:

```
react
 react-dom
```

`aem-clientlib-generator` viene utilizzato per rendere automatica la creazione di librerie client come parte del processo di compilazione.

`"aem-clientlib-generator": "^1.4.1",`

Ulteriori dettagli sul generatore [aem-clientlib sono disponibili su GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versione minima di `aem-clientlib-generator` richiesta è 1.4.1.

`aem-clientlib-generator` è configurato nel file `clientlib.config.js` come segue.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Generazione in corso {#building}

In realtà, la creazione dell&#39;app utilizza [Webpack](https://webpack.js.org/) per la transpilazione oltre a aem-clientlib-generator per la creazione automatica della libreria client. Pertanto, il comando build sarà simile al seguente:

`"build": "webpack && clientlib --verbose"`

Una volta generato, il pacchetto può essere caricato in un’istanza di AEM.

### Archetipo di progetto AEM {#aem-project-archetype}

Qualsiasi progetto AEM deve utilizzare l’[archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Struttura dell&#39;applicazione {#application-structure}

Se includi le dipendenze e crei l’app come descritto in precedenza, riceverai un pacchetto di applicazioni a pagina singola funzionante che puoi caricare nell’istanza di AEM.

La sezione successiva di questo documento illustra come è strutturata un’applicazione a pagina singola in AEM, i file importanti che guidano l’applicazione e come funzionano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione sono basati sullo stesso concetto.

### index.js {#index-js}

Il punto di ingresso nell&#39;applicazione a pagina singola è il file `index.js` qui mostrato semplificato per concentrarsi sul contenuto importante.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

La funzione principale di `index.js` consiste nell&#39;utilizzare la funzione `ReactDOM.render` per determinare dove inserire l&#39;applicazione nel DOM.

Si tratta di un utilizzo standard di questa funzione, non specifico di questa app di esempio.

#### Creazione di istanze statiche {#static-instantiation}

Quando il componente viene creato in modo statico utilizzando il modello di componente (ad esempio, JSX), il valore deve essere trasmesso dal modello alle proprietà del componente.

### App.js {#app-js}

Tramite il rendering dell&#39;app, `index.js` chiama `App.js`, che viene mostrato qui in una versione semplificata per concentrarsi sul contenuto importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` serve principalmente per eseguire il wrapping dei componenti radice che compongono l&#39;app. Il punto di ingresso di qualsiasi app è la pagina.

### Page.js {#page-js}

Tramite il rendering della pagina, `App.js` chiama `Page.js` elencato qui in una versione semplificata.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

In questo esempio la classe `AppPage` estende `Page`, che contiene i metodi di contenuto interno che possono quindi essere utilizzati.

`Page` acquisisce la rappresentazione JSON del modello di pagina ed elabora il contenuto per racchiudere/decorare ogni elemento della pagina. Ulteriori dettagli su `Page` sono disponibili nel documento [Blueprint SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

Con il rendering della pagina, è possibile eseguire il rendering dei componenti come `Image.js`, come mostrato di seguito.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

L’idea centrale delle applicazioni a pagina singola in AEM è quella di mappare i componenti delle applicazioni a pagina singola ai componenti di AEM e di aggiornare il componente quando il contenuto viene modificato (e viceversa). Per un riepilogo di questo modello di comunicazione, vedere il documento [Panoramica dell&#39;editor SPA](/help/sites-developing/spa-overview.md).

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

Il metodo `MapTo` associa il componente SPA al componente AEM. Supporta l’utilizzo di una singola stringa o di un array di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce ad abilitare le funzionalità di creazione di un componente fornendo i metadati necessari all&#39;editor per generare segnaposto

Se non è presente alcun contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà passate dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono passati dinamicamente come proprietà del componente.

## Esportazione di contenuti modificabili {#exporting-editable-content}

Puoi esportare un componente e mantenerlo modificabile.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

La funzione `MapTo` restituisce un `Component` che è il risultato di una composizione che estende il `PageClass` fornito con i nomi e gli attributi della classe che abilitano l&#39;authoring. Questo componente può essere esportato in un secondo momento e istanziato nel markup dell’applicazione.

Quando viene esportato utilizzando le funzioni `MapTo` o `withModel`, il componente `Page` è racchiuso in un componente `ModelProvider` che fornisce l&#39;accesso ai componenti standard alla versione più recente del modello di pagina o a una posizione precisa nel modello di pagina.

Per ulteriori informazioni, vedi il documento [Blueprint SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>Per impostazione predefinita, quando si utilizza la funzione `withModel` si riceve l&#39;intero modello del componente.

## Condivisione di informazioni tra i componenti SPA {#sharing-information-between-spa-components}

La condivisione delle informazioni è regolarmente necessaria per i componenti di un’applicazione a pagina singola. Esistono diversi modi consigliati per farlo, elencati di seguito in ordine crescente di complessità.

* **Opzione 1:** Centralizza la logica e la trasmissione ai componenti necessari, ad esempio, utilizzando React Context.
* **Opzione 2:** Condividere gli stati dei componenti utilizzando una libreria di stati come Redux.
* **Opzione 3:** Sfrutta la gerarchia degli oggetti personalizzando ed estendendo il componente contenitore.

## Passaggi successivi {#next-steps}

Per una guida dettagliata alla creazione di un&#39;applicazione a pagina singola personalizzata, vedi [Guida introduttiva all&#39;editor di applicazioni a pagina singola di AEM - Esercitazione eventi WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=it).

Per ulteriori informazioni su come organizzare lo sviluppo di applicazioni a pagina singola per AEM, vedere l&#39;articolo [Sviluppo di applicazioni a pagina singola per AEM](/help/sites-developing/spa-architecture.md).

Per ulteriori dettagli sul mapping tra modello dinamico e componente e sul suo funzionamento all&#39;interno delle applicazioni a pagina singola in AEM, vedere l&#39;articolo [Mapping tra modello dinamico e componente per applicazioni a pagina singola](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desideri implementare le applicazioni a pagina singola in AEM per un framework diverso da React o Angular o semplicemente approfondire il funzionamento di SPA SDK for AEM, consulta l&#39;articolo [Blueprint SPA](/help/sites-developing/spa-blueprint.md).
