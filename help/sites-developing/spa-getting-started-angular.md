---
title: Guida introduttiva dell’SPA nell’AEM - Angular
description: Questo articolo presenta un esempio di applicazione per l’SPA, spiega come viene creata e come iniziare subito a utilizzare il proprio SPA utilizzando il framework Angular.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 5%

---

# Guida introduttiva dell’SPA nell’AEM - Angular{#getting-started-with-spas-in-aem-angular}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando framework SPA e gli autori desiderano modificare facilmente i contenuti all’interno dell’AEM per un sito creato utilizzando framework SPA.

La funzione di authoring dell’SPA offre una soluzione completa per il supporto dell’SPA nell’ambito dell’AEM. Questo articolo presenta un’applicazione SPA semplificata sul framework Angular, spiega come viene creato e come iniziare a utilizzare il tuo SPA in modo rapido.

>[!NOTE]
>
>Questo articolo si basa sul framework Angular. Per il documento corrispondente per il framework React vedere [Guida introduttiva all&#39;SPA nell&#39;AEM - React](/help/sites-developing/spa-getting-started-react.md).

>[!NOTE]
>
>L’editor SPA è la soluzione consigliata per i progetti che richiedono il rendering lato client basato sul framework SPA (ad esempio, React o Angular).

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di un semplice SPA e il minimo che è necessario sapere per rendere il vostro funzionamento.

Per maggiori dettagli sul funzionamento dell’SPA nell’AEM, consulta i seguenti documenti:

* [Introduzione alla SPA e procedura dettagliata](/help/sites-developing/spa-walkthrough.md)
* [Introduzione all’authoring di SPA](/help/sites-developing/spa-overview.md)
* [Blueprint SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un SPA, questi devono essere memorizzati nell’AEM ed essere esposti dal modello di contenuto.
>
>Un SPA sviluppato al di fuori dell&#39;AEM non sarà credibile se non rispetta il contratto tipo di contenuto.

Questo documento illustra la struttura di un SPA semplificato e il suo funzionamento, per consentirti di applicare questa conoscenza al tuo SPA.

## Dipendenze, configurazione e generazione {#dependencies-configuration-and-building}

Oltre alla prevista dipendenza degli Angular, l&#39;SPA di esempio può utilizzare librerie aggiuntive per rendere più efficiente la creazione dell&#39;SPA.

### Dipendenze {#dependencies}

Il file `package.json` definisce i requisiti del pacchetto SPA complessivo. Le dipendenze minime richieste dall’AEM sono elencate qui.

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

Una volta generato, il pacchetto può essere caricato in un’istanza AEM.

### Archetipo progetto AEM {#aem-project-archetype}

Qualsiasi progetto AEM deve utilizzare l’[archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Struttura dell&#39;applicazione {#application-structure}

L’inclusione delle dipendenze e la creazione dell’app come descritto in precedenza ti lasceranno con un pacchetto SPA funzionante che puoi caricare nell’istanza AEM.

La sezione successiva di questo documento illustra la struttura di un SPA nell’AEM, i file importanti che guidano l’applicazione e il modo in cui lavorano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione sono basati sullo stesso concetto.

### app.module.ts {#app-module-ts}

Il punto di ingresso nell&#39;SPA è il file `app.module.ts` qui mostrato semplificato per concentrarsi sul contenuto importante.

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

L&#39;idea centrale dell&#39;SPA nell&#39;AEM è l&#39;idea di mappare i componenti dell&#39;SPA ai componenti dell&#39;AEM e di aggiornare il componente quando il contenuto viene modificato (e viceversa). Per un riepilogo di questo modello di comunicazione, vedere il documento [Panoramica dell&#39;editor SPA](/help/sites-developing/spa-overview.md).

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

Il metodo `MapTo` mappa il componente SPA al componente AEM. Supporta l’utilizzo di una singola stringa o di un array di stringhe.

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

## Condivisione di informazioni tra i componenti dell’SPA {#sharing-information-between-spa-components}

La condivisione delle informazioni è regolarmente necessaria per i componenti di un’applicazione a pagina singola. Esistono diversi modi consigliati per farlo, elencati di seguito in ordine crescente di complessità.

* **Opzione 1:** Centralizza la logica e la trasmissione ai componenti necessari, ad esempio, utilizzando una classe util come soluzione puramente orientata agli oggetti.
* **Opzione 2:** condividere gli stati dei componenti utilizzando una libreria di stati come NgRx.
* **Opzione 3:** Sfrutta la gerarchia degli oggetti personalizzando ed estendendo il componente contenitore.

## Passaggi successivi {#next-steps}

Per una guida dettagliata alla creazione di un proprio SPA, consulta [Guida introduttiva all&#39;Editor SPA dell&#39;AEM - Esercitazione eventi WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=it).

Per ulteriori informazioni su come organizzare lo sviluppo di SPA per AEM, vedere l&#39;articolo [Sviluppo di SPA per AEM](/help/sites-developing/spa-architecture.md).

Per ulteriori dettagli sulla mappatura da modello dinamico a componente e sul suo funzionamento all&#39;interno dell&#39;SPA nell&#39;AEM, vedere l&#39;articolo [Mappatura da modello dinamico a componente per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desideri implementare l&#39;SPA nell&#39;AEM per un framework diverso da React o Angular o semplicemente approfondire il funzionamento dell&#39;SDK SPA per l&#39;AEM, consulta l&#39;articolo [Blueprint SPA](/help/sites-developing/spa-blueprint.md).
