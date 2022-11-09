---
title: Guida introduttiva a SPA in AEM - React
seo-title: Getting Started with SPAs in AEM - React
description: Questo articolo presenta un esempio di applicazione SPA, spiega come viene assemblato e ti consente di iniziare a usare rapidamente il tuo SPA utilizzando il framework React.
seo-description: This article presents a sample SPA application, explains how it is put together, and allows you to get up-and-running with your own SPA quickly using the React framework.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 3%

---

# Guida introduttiva a SPA in AEM - React{#getting-started-with-spas-in-aem-react}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano poter creare siti utilizzando framework SPA e gli autori desiderano modificare i contenuti all’interno di AEM per un sito creato utilizzando framework SPA.

La funzione di authoring SPA offre una soluzione completa per supportare SPA all’interno di AEM. Questo articolo presenta un&#39;applicazione SPA semplificata sul framework React, spiega come viene messo insieme, che consente di iniziare rapidamente a usare i propri SPA.

>[!NOTE]
>
>Questo articolo si basa sul quadro di React. Per il documento corrispondente per il framework di Angular vedi [Guida introduttiva a SPA in AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>L’editor di SPA è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad esempio, React o Angular).

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di un SPA semplice e il minimo che devi sapere per far funzionare il tuo.

Per ulteriori dettagli sul funzionamento SPA in AEM, consulta i seguenti documenti:

* [Introduzione a SPA e procedura dettagliata](/help/sites-developing/spa-walkthrough.md)
* [Introduzione all’authoring SPA](/help/sites-developing/spa-overview.md)
* [Blueprint SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un SPA, i contenuti devono essere memorizzati in AEM ed essere esposti dal modello di contenuto.
>
>Un SPA sviluppato al di fuori di AEM non sarà autorizzabile se non rispetta il contratto relativo al modello di contenuto.

Questo documento illustra la struttura di un SPA semplificato creato utilizzando il framework React e illustra come funziona in modo da poter applicare questa comprensione al proprio SPA.

## Dipendenze, configurazione e creazione {#dependencies-configuration-and-building}

Oltre alla dipendenza React prevista, l’SPA di esempio può sfruttare librerie aggiuntive per rendere più efficiente la creazione dell’SPA.

### Dipendenze {#dependencies}

La `package.json` Il file definisce i requisiti del pacchetto SPA globale. Le dipendenze minime AEM per un SPA di lavoro sono elencate qui.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Poiché questo esempio si basa sul quadro React, esistono due dipendenze specifiche React che sono obbligatorie nel `package.json` file:

```
react
 react-dom
```

La `aem-clientlib-generator` viene sfruttato per rendere automatica la creazione di librerie client come parte del processo di compilazione.

`"aem-clientlib-generator": "^1.4.1",`

Maggiori dettagli sono disponibili [su GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>Versione minima del `aem-clientlib-generator` obbligatorio: 1.4.1.

La `aem-clientlib-generator` è configurato in `clientlib.config.js` file come segue.

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

### Creazione di {#building}

In realtà, la creazione di app sfrutta [Webpack](https://webpack.js.org/) per la trasformazione in aggiunta al generatore aem-clientlib-per la creazione automatica della libreria client. Pertanto, il comando di compilazione sarà simile a:

`"build": "webpack && clientlib --verbose"`

Una volta generato, il pacchetto può essere caricato in un&#39;istanza AEM.

### Archetipo progetto AEM {#aem-project-archetype}

Qualsiasi progetto AEM deve sfruttare [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Struttura dell&#39;applicazione {#application-structure}

L’inclusione delle dipendenze e la creazione dell’app come descritto in precedenza ti lasceranno con un pacchetto di SPA funzionante che puoi caricare nella tua istanza AEM.

La sezione successiva di questo documento illustra la struttura di un SPA in AEM, i file importanti che guidano l&#39;applicazione e il modo in cui funzionano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione sono basati sullo stesso concetto.

### index.js {#index-js}

Il punto di ingresso nel SPA è ovviamente il `index.js` il file mostrato qui è stato semplificato per concentrarsi sul contenuto importante.

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

La funzione principale di `index.js` utilizza `ReactDOM.render` per determinare dove nel DOM inserire l&#39;applicazione.

Si tratta di un utilizzo standard di questa funzione, non univoco per questa app di esempio.

#### Istanza statica {#static-instantiation}

Quando il componente viene istanziato staticamente utilizzando il modello di componente (ad esempio JSX), il valore deve essere passato dal modello alle proprietà del componente.

### App.js {#app-js}

Rendering dell’app `index.js` chiama `App.js`, che viene qui mostrato in una versione semplificata per concentrarsi sul contenuto importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` utilizza principalmente per racchiudere i componenti principali che compongono l’app. Il punto di ingresso di qualsiasi app è la pagina.

### Page.js {#page-js}

Rendering della pagina `App.js` chiama `Page.js` elencati in una versione semplificata.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

In questo esempio `AppPage` Estensioni di classe `Page`, che contiene i metodi di contenuto interno che possono essere utilizzati.

La `Page` acquisisce la rappresentazione JSON del modello di pagina ed elabora il contenuto per racchiudere/decorare ogni elemento della pagina. Maggiori dettagli `Page` disponibile nel documento [Blueprint SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

Con il rendering della pagina, i componenti come `Image.js` come mostrato qui, è possibile renderizzarlo.

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

L’idea centrale di SPA in AEM è quella di mappare SPA componenti ai componenti AEM e aggiornare il componente quando il contenuto viene modificato (e viceversa). Vedere il documento [Panoramica dell’editor di SPA](/help/sites-developing/spa-overview.md) per una sintesi di questo modello di comunicazione.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

La `MapTo` mappa il componente SPA al componente AEM. Supporta l&#39;uso di una singola stringa o di una matrice di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce ad abilitare le funzionalità di authoring di un componente fornendo i metadati necessari affinché l’editor generi segnaposti

In assenza di contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà trasmesse dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono trasmessi dinamicamente come proprietà del componente.

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

La `MapTo` restituisce un `Component` che è il risultato di una composizione che estende il `PageClass` con i nomi e gli attributi della classe che abilitano l&#39;authoring. Questo componente può essere esportato in un secondo momento per essere istanziato nel markup dell’applicazione.

Quando viene esportato utilizzando la variabile `MapTo` o `withModel` le funzioni `Page` è racchiuso in un `ModelProvider` che fornisce ai componenti standard l’accesso alla versione più recente del modello di pagina o a una posizione precisa nel modello di pagina.

Per ulteriori informazioni, consulta la sezione [Documento Blueprint SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>Per impostazione predefinita viene visualizzato l’intero modello del componente quando si utilizza il `withModel` funzione .

## Condivisione Di Informazioni Tra I Componenti SPA {#sharing-information-between-spa-components}

È regolarmente necessario che i componenti all’interno di un’applicazione a pagina singola condividano informazioni. Ci sono diversi modi raccomandati per farlo, elencati come segue in ordine crescente di complessità.

* **Opzione 1:** Centralizza la logica e la trasmissione ai componenti necessari, ad esempio utilizzando il contesto di reazione.
* **Opzione 2:** Condividere gli stati dei componenti utilizzando una libreria di stati come Redux.
* **Opzione 3:** Sfrutta la gerarchia degli oggetti personalizzando ed estendendo il componente contenitore .

## Passaggi successivi {#next-steps}

Per una guida dettagliata alla creazione di un tuo SPA, consulta la sezione [Guida introduttiva all’editor di SPA AEM - Tutorial eventi WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=it).

Per ulteriori informazioni su come organizzarsi per sviluppare SPA per AEM vedere l&#39;articolo [Sviluppo di SPA per AEM](/help/sites-developing/spa-architecture.md).

Per ulteriori dettagli sul modello dinamico per la mappatura dei componenti e su come funziona all’interno di SPA in AEM, consulta l’articolo [Mappatura dinamica da modello a componente per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desideri implementare SPA in AEM per un framework diverso da React o Angular o desideri semplicemente approfondire il funzionamento dell’SDK SPA per AEM, consulta [Blueprint SPA](/help/sites-developing/spa-blueprint.md) articolo.
