---
title: Guida introduttiva alla SPA in AEM - React
seo-title: Guida introduttiva alla SPA in AEM - React
description: Questo articolo presenta un esempio SPA applicazione, spiega come viene assemblata e consente di iniziare rapidamente a usare la propria SPA utilizzando la struttura React.
seo-description: Questo articolo presenta un esempio SPA applicazione, spiega come viene assemblata e consente di iniziare rapidamente a usare la propria SPA utilizzando la struttura React.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 1%

---


# Guida introduttiva alla SPA in AEM - React{#getting-started-with-spas-in-aem-react}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando SPA framework e gli autori desiderano modificare i contenuti all&#39;interno di AEM per un sito creato utilizzando SPA framework.

La funzione di authoring SPA offre una soluzione completa per SPA di supporto in AEM. Questo articolo presenta un&#39;applicazione SPA semplificata nel framework React, spiega come viene assemblata, consentendo di iniziare rapidamente a usare i propri SPA.

>[!NOTE]
>
>Questo articolo si basa sul quadro di React. Per il documento corrispondente per il framework Angular, vedere [Guida introduttiva alle SPA in AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad es. React o Angular).

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di un semplice SPA e il minimo che devi sapere per far funzionare il tuo.

Per maggiori dettagli sul funzionamento SPA in AEM, consulta i documenti seguenti:

* [Introduzione SPA e Procedura dettagliata](/help/sites-developing/spa-walkthrough.md)
* [Introduzione all’authoring SPA](/help/sites-developing/spa-overview.md)
* [Blueprint SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un SPA, i contenuti devono essere memorizzati in AEM ed essere esposti dal modello di contenuto.
>
>Un SPA sviluppato al di fuori di AEM non sarà autorizzabile se non rispetta il contratto per il modello di contenuto.

Questo documento illustra la struttura di un SPA semplificato creato con il framework React e illustra come funziona, in modo da poter applicare questa comprensione ai SPA.

## Dipendenze, configurazione e generazione {#dependencies-configuration-and-building}

Oltre alla dipendenza React prevista, l’SPA di esempio può sfruttare librerie aggiuntive per rendere più efficiente la creazione del SPA.

### Dipendenze {#dependencies}

Il file `package.json` definisce i requisiti del pacchetto SPA complessivo. Le dipendenze AEM minime per un SPA di lavoro sono elencate di seguito.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Poiché questo esempio è basato sul framework React, nel file `package.json` sono presenti due dipendenze specifiche di React obbligatorie:

```
react
 react-dom
```

`aem-clientlib-generator` è stata utilizzata per rendere automatica la creazione di librerie client come parte del processo di creazione.

`"aem-clientlib-generator": "^1.4.1",`

Per maggiori informazioni, vedere [su GitHub qui](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versione minima della `aem-clientlib-generator` richiesta è 1.4.1.

La `aem-clientlib-generator` è configurata nel file `clientlib.config.js` come segue.

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

La creazione dell&#39;app si basa su [Webpack](https://webpack.js.org/) per la traslazione oltre al generatore aem-clientlib-generator per la creazione automatica della libreria client. Il comando build sarà quindi simile a:

`"build": "webpack && clientlib --verbose"`

Una volta creato, il pacchetto può essere caricato in un&#39;istanza AEM.

### AEM Project Archetype {#aem-project-archetype}

Qualsiasi progetto AEM deve sfruttare il [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta SPA progetti utilizzando React o Angular e sfrutta l&#39;SDK SPA.

## Struttura dell&#39;applicazione {#application-structure}

L&#39;inclusione delle dipendenze e la creazione dell&#39;app come descritto in precedenza vi lasceranno con un pacchetto SPA funzionante che potete caricare nell&#39;istanza AEM.

La sezione successiva di questo documento illustra la struttura di un SPA in AEM, i file importanti che guidano l&#39;applicazione e la modalità di funzionamento dell&#39;applicazione.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione si basano sullo stesso concetto.

### index.js {#index-js}

Il punto di ingresso nel SPA è ovviamente il file `index.js` mostrato qui semplificato per concentrarsi sul contenuto importante.

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

La funzione principale di `index.js` consiste nell&#39;utilizzare la funzione `ReactDOM.render` per determinare dove nel DOM inserire l&#39;applicazione.

Si tratta di un utilizzo standard di questa funzione, non univoco per questa app di esempio.

#### Istanziazione statica {#static-instantiation}

Quando un’istanza del componente viene creata in modo statico utilizzando il modello di componente (ad esempio, JSX), il valore deve essere passato dal modello alle proprietà del componente.

### App.js {#app-js}

Eseguendo il rendering dell&#39;app, `index.js` richiama `App.js`, che viene visualizzata in una versione semplificata per concentrarvi sul contenuto importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` serve principalmente per racchiudere i componenti principali che compongono l&#39;app. Il punto di ingresso di qualsiasi app è la pagina.

### Page.js {#page-js}

Rendendo la pagina, `App.js` esegue le chiamate `Page.js` elencate in una versione semplificata.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

In questo esempio la classe `AppPage` estende `Page`, che contiene i metodi di contenuto interno che possono essere utilizzati.

L&#39; `Page` acquisisce la rappresentazione JSON del modello di pagina ed elabora il contenuto per racchiudere/decorare ogni elemento della pagina. Ulteriori dettagli sulla `Page` si trovano nel documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

Con la pagina sottoposta a rendering, è possibile eseguire il rendering dei componenti come `Image.js`, come illustrato di seguito.

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

L’idea centrale di SPA in AEM è la mappatura SPA componenti a componenti AEM e l’aggiornamento del componente quando il contenuto viene modificato (e viceversa). Per un riepilogo di questo modello di comunicazione, vedere il documento [SPA Editor Overview](/help/sites-developing/spa-overview.md).

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

Il metodo `MapTo` mappa il componente SPA al componente AEM. Supporta l&#39;uso di una singola stringa o di una matrice di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce a abilitare le funzionalità di authoring di un componente fornendo i metadati necessari affinché l’editor generi i segnaposto

In assenza di contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà trasmesse dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono passati in modo dinamico come proprietà del componente.

## Esportazione di contenuto modificabile {#exporting-editable-content}

Potete esportare un componente e mantenerlo modificabile.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

La funzione `MapTo` restituisce un `Component` che è il risultato di una composizione che estende l&#39;elemento `PageClass` fornito con i nomi e gli attributi di classe che abilitano l&#39;authoring. Questo componente può essere esportato in un secondo momento per essere istanziato nella marcatura dell’applicazione.

Quando viene esportato utilizzando le funzioni `MapTo` o `withModel`, il componente `Page` è racchiuso con un componente `ModelProvider` che consente ai componenti standard di accedere alla versione più recente del modello di pagina o a una posizione precisa in tale modello di pagina.

Per ulteriori informazioni, vedere il documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>Per impostazione predefinita, quando si utilizza la funzione `withModel` si riceve l&#39;intero modello del componente.

## Condivisione delle informazioni tra SPA componenti {#sharing-information-between-spa-components}

È necessario che i componenti all’interno di un’applicazione a pagina singola condividano informazioni. Ci sono diversi modi consigliati di fare questo, elencati come segue in ordine crescente di complessità.

* **Opzione 1:** Centralizzare la logica e la trasmissione ai componenti necessari, ad esempio utilizzando React Context.
* **Opzione 2:** condividere gli stati dei componenti utilizzando una libreria di stato come Redux.
* **Opzione 3:** Sfruttare la gerarchia degli oggetti personalizzando ed estendendo il componente contenitore.

## Passaggi successivi {#next-steps}

Per una guida passo-passo alla creazione di SPA personali, vedere la [Guida introduttiva all&#39;editor SPA AEM - Esercitazione eventi WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Per ulteriori informazioni su come organizzarsi per sviluppare SPA per AEM vedere l&#39;articolo [Sviluppo SPA per AEM](/help/sites-developing/spa-architecture.md).

Per ulteriori dettagli sulla mappatura del modello dinamico a componente e sul suo funzionamento all&#39;interno SPA in AEM, vedere l&#39;articolo [Mappatura del modello dinamico a componente per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desideri implementare SPA in AEM per un framework diverso da React o Angular o desideri semplicemente approfondire il funzionamento dell&#39;SDK SPA per AEM, fai riferimento all&#39;articolo [SPA Blueprint](/help/sites-developing/spa-blueprint.md).
