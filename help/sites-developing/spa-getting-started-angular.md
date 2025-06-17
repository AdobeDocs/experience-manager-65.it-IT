---
title: Guida introduttiva alle applicazioni a pagina singola in AEM - Angular
description: Questo articolo presenta un esempio di applicazione SPA, spiega come viene creata e come iniziare subito a utilizzare un’applicazione SPA personale con il framework Angular.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 5%

---


# Guida introduttiva alle applicazioni a pagina singola in AEM - Angular{#getting-started-with-spas-in-aem-angular}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando framework SPA e gli autori desiderano modificare facilmente i contenuti all’interno di AEM per un sito creato utilizzando framework SPA.

La funzione di authoring di applicazioni a pagina singola offre una soluzione completa per il supporto di applicazioni a pagina singola in AEM. Questo articolo presenta un’applicazione SPA semplificata sul framework Angular, spiega come viene creata e come iniziare subito a utilizzare un’applicazione SPA personale.

>[!NOTE]
>
>Questo articolo si basa sul framework Angular. Per il documento corrispondente per il framework React vedi [Guida introduttiva alle applicazioni a pagina singola in AEM - React](/help/sites-developing/spa-getting-started-react.md).

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

Questo documento illustra la struttura di un’applicazione a pagina singola semplificata e il suo funzionamento, consentendoti di applicare questa conoscenza all’applicazione a pagina singola.

## Dipendenze, configurazione e generazione {#dependencies-configuration-and-building}

Oltre alla dipendenza prevista da Angular, l’applicazione a pagina singola di esempio può utilizzare librerie aggiuntive per rendere più efficiente la creazione dell’applicazione a pagina singola.

### Dipendenze {#dependencies}

Il file `package.json` definisce i requisiti del pacchetto SPA complessivo. Le dipendenze minime richieste da AEM sono elencate qui.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

`aem-clientlib-generator` viene utilizzato per rendere automatica la creazione di librerie client come parte del processo di compilazione.

`"aem-clientlib-generator": "^1.4.1",`

Ulteriori dettagli su [aem-clientlib-generator sono disponibili su GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versione minima di `aem-clientlib-generator` richiesta è 1.4.1.

`aem-clientlib-generator` è configurato nel file `clientlib.config.js` come segue.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

`"build": "ng build --build-optimizer=false && clientlib",`

Una volta generato, il pacchetto può essere caricato in un’istanza di AEM.

### Archetipo di progetto AEM {#aem-project-archetype}

Qualsiasi progetto AEM deve utilizzare l’[archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Struttura dell&#39;applicazione {#application-structure}

Se includi le dipendenze e crei l’app come descritto in precedenza, riceverai un pacchetto di applicazioni a pagina singola funzionante che puoi caricare nell’istanza di AEM.

La sezione successiva di questo documento illustra come è strutturata un’applicazione a pagina singola in AEM, i file importanti che guidano l’applicazione e come funzionano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione sono basati sullo stesso concetto.

### app.module.ts {#app-module-ts}

Il punto di ingresso nell&#39;applicazione a pagina singola è il file `app.module.ts` qui mostrato semplificato per concentrarsi sul contenuto importante.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

Il file `app.module.ts` è il punto iniziale dell&#39;app e contiene la configurazione iniziale del progetto e utilizza `AppComponent` per avviare l&#39;app.

#### Creazione di istanze statiche {#static-instantiation}

Quando il componente viene creato in modo statico utilizzando la maschera del componente, il valore deve essere passato dal modello alle proprietà del componente. I valori del modello vengono passati come attributi, per poi essere disponibili come proprietà dei componenti.

### app.component.ts {#app-component-ts}

Una volta avviato `AppComponent`, `app.module.ts` può inizializzare l&#39;app, che viene qui mostrata in una versione semplificata per concentrarsi sul contenuto importante.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

Elaborando la pagina, `app.component.ts` chiama `main-content.component.ts` elencato qui in una versione semplificata.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

`MainComponent` acquisisce la rappresentazione JSON del modello di pagina ed elabora il contenuto per racchiudere/decorare ogni elemento della pagina. Ulteriori dettagli su `Page` sono disponibili nel documento [Blueprint SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

`Page` è composto da componenti. Con il JSON acquisito, `Page` può elaborare tali componenti come `image.component.ts`, come mostrato qui.

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

L’idea centrale delle applicazioni a pagina singola in AEM è quella di mappare i componenti delle applicazioni a pagina singola ai componenti di AEM e di aggiornare il componente quando il contenuto viene modificato (e viceversa). Per un riepilogo di questo modello di comunicazione, vedere il documento [Panoramica dell&#39;editor SPA](/help/sites-developing/spa-overview.md).

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

Il metodo `MapTo` associa il componente SPA al componente AEM. Supporta l’utilizzo di una singola stringa o di un array di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce ad abilitare le funzionalità di creazione di un componente fornendo i metadati necessari all&#39;editor per generare segnaposto

Se non è presente alcun contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà passate dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono passati dinamicamente come proprietà del componente.

### image.component.html {#image-component-html}

Infine, è possibile eseguire il rendering dell&#39;immagine in `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Condivisione di informazioni tra i componenti SPA {#sharing-information-between-spa-components}

La condivisione delle informazioni è regolarmente necessaria per i componenti di un’applicazione a pagina singola. Esistono diversi modi consigliati per farlo, elencati di seguito in ordine crescente di complessità.

* **Opzione 1:** Centralizza la logica e la trasmissione ai componenti necessari, ad esempio, utilizzando una classe util come soluzione puramente orientata agli oggetti.
* **Opzione 2:** condividere gli stati dei componenti utilizzando una libreria di stati come NgRx.
* **Opzione 3:** Sfrutta la gerarchia degli oggetti personalizzando ed estendendo il componente contenitore.

## Passaggi successivi {#next-steps}

Per una guida dettagliata alla creazione di un&#39;applicazione a pagina singola personalizzata, vedi [Guida introduttiva all&#39;editor di applicazioni a pagina singola di AEM - Esercitazione eventi WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=it).

Per ulteriori informazioni su come organizzare lo sviluppo di applicazioni a pagina singola per AEM, vedere l&#39;articolo [Sviluppo di applicazioni a pagina singola per AEM](/help/sites-developing/spa-architecture.md).

Per ulteriori dettagli sul mapping tra modello dinamico e componente e sul suo funzionamento all&#39;interno delle applicazioni a pagina singola in AEM, vedere l&#39;articolo [Mapping tra modello dinamico e componente per applicazioni a pagina singola](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desideri implementare le applicazioni a pagina singola in AEM per un framework diverso da React o Angular o semplicemente approfondire il funzionamento di SPA SDK for AEM, consulta l&#39;articolo [Blueprint SPA](/help/sites-developing/spa-blueprint.md).
