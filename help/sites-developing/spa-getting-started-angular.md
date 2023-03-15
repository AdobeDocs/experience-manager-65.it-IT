---
title: Guida introduttiva a SPA in AEM - Angular
seo-title: Getting Started with SPAs in AEM - Angular
description: Questo articolo presenta un esempio di applicazione SPA, spiega come viene assemblato e ti consente di iniziare rapidamente a usare il tuo SPA utilizzando il framework di Angular.
seo-description: This article presents a sample SPA application, explains how it is put together, and allows you to get up-and-running with your own SPA quickly using the Angular framework.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 6%

---

# Guida introduttiva a SPA in AEM - Angular{#getting-started-with-spas-in-aem-angular}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano poter creare siti utilizzando framework SPA e gli autori desiderano modificare i contenuti all’interno di AEM per un sito creato utilizzando framework SPA.

La funzione di authoring SPA offre una soluzione completa per supportare SPA all’interno di AEM. Questo articolo presenta un&#39;applicazione SPA semplificata sul framework di Angular, spiega come viene messo insieme, che ti permette di iniziare a lavorare rapidamente con il tuo SPA.

>[!NOTE]
>
>Questo articolo si basa sul quadro Angular. Per il documento corrispondente per il quadro React vedi [Guida introduttiva a SPA in AEM - React](/help/sites-developing/spa-getting-started-react.md).

>[!NOTE]
>
>L’editor di SPA è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad esempio, React o Angular).

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di un SPA semplice e il minimo che devi sapere per far funzionare il tuo.

Per ulteriori dettagli sul funzionamento SPA in AEM, consulta i seguenti documenti:

* [Introduzione alla SPA e procedura dettagliata](/help/sites-developing/spa-walkthrough.md)
* [Introduzione all’authoring SPA](/help/sites-developing/spa-overview.md)
* [Blueprint SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un SPA, i contenuti devono essere memorizzati in AEM ed essere esposti dal modello di contenuto.
>
>Un SPA sviluppato al di fuori di AEM non sarà autorizzabile se non rispetta il contratto relativo al modello di contenuto.

Questo documento illustra la struttura di un SPA semplificato e illustra come funziona in modo da poter applicare questa comprensione al proprio SPA.

## Dipendenze, configurazione e creazione {#dependencies-configuration-and-building}

Oltre alla dipendenza prevista dall’Angular, l’SPA di esempio può sfruttare librerie aggiuntive per rendere più efficiente la creazione dell’SPA.

### Dipendenze {#dependencies}

La `package.json` Il file definisce i requisiti del pacchetto SPA globale. Le dipendenze AEM minime richieste sono elencate qui.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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

### Creazione di {#building}

In realtà, la creazione di app sfrutta [Webpack](https://webpack.js.org/) per la trasformazione in aggiunta al generatore aem-clientlib-per la creazione automatica della libreria client. Pertanto, il comando di compilazione sarà simile a:

`"build": "ng build --build-optimizer=false && clientlib",`

Una volta generato, il pacchetto può essere caricato in un&#39;istanza AEM.

### Archetipo progetto AEM {#aem-project-archetype}

Qualsiasi progetto AEM deve utilizzare l’[archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Struttura dell&#39;applicazione {#application-structure}

L’inclusione delle dipendenze e la creazione dell’app come descritto in precedenza ti lasceranno con un pacchetto di SPA funzionante che puoi caricare nella tua istanza AEM.

La sezione successiva di questo documento illustra la struttura di un SPA in AEM, i file importanti che guidano l&#39;applicazione e il modo in cui funzionano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione sono basati sullo stesso concetto.

### app.module.ts {#app-module-ts}

Il punto di ingresso nel SPA è il `app.module.ts` il file mostrato qui è stato semplificato per concentrarsi sul contenuto importante.

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

La `app.module.ts` è il punto iniziale dell’app e contiene la configurazione iniziale del progetto e utilizza `AppComponent` per avviare l&#39;app.

#### Istanza statica {#static-instantiation}

Quando un’istanza del componente viene creata in modo statico utilizzando il modello di componente, il valore deve essere trasmesso dal modello alle proprietà del componente. I valori del modello vengono passati come attributi per essere successivamente disponibili come proprietà del componente.

### app.component.ts {#app-component-ts}

Una volta `app.module.ts` bootstrap `AppComponent`, può quindi inizializzare l’app, che viene visualizzata qui in una versione semplificata per concentrarti sul contenuto importante.

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

Elaborando la pagina, `app.component.ts` chiama `main-content.component.ts` qui in una versione semplificata.

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

La `MainComponent` acquisisce la rappresentazione JSON del modello di pagina ed elabora il contenuto per racchiudere/decorare ogni elemento della pagina. Maggiori dettagli `Page` disponibile nel documento [Blueprint SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

La `Page` è composto da componenti. Con il JSON acquisito, il `Page` può elaborare componenti quali `image.component.ts` come mostrato qui.

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

L’idea centrale di SPA in AEM è quella di mappare SPA componenti ai componenti AEM e aggiornare il componente quando il contenuto viene modificato (e viceversa). Vedere il documento [Panoramica dell’editor di SPA](/help/sites-developing/spa-overview.md) per una sintesi di questo modello di comunicazione.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

La `MapTo` mappa il componente SPA al componente AEM. Supporta l&#39;uso di una singola stringa o di una matrice di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce ad abilitare le funzionalità di authoring di un componente fornendo i metadati necessari affinché l’editor generi segnaposti

In assenza di contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà trasmesse dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono trasmessi dinamicamente come proprietà del componente.

### image.component.html {#image-component-html}

Infine, è possibile eseguire il rendering dell&#39;immagine `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Condivisione Di Informazioni Tra I Componenti SPA {#sharing-information-between-spa-components}

È regolarmente necessario che i componenti all’interno di un’applicazione a pagina singola condividano informazioni. Ci sono diversi modi raccomandati per farlo, elencati come segue in ordine crescente di complessità.

* **Opzione 1:** Centralizzare la logica e la trasmissione ai componenti necessari, ad esempio utilizzando una classe util come soluzione puramente orientata agli oggetti.
* **Opzione 2:** Condividere gli stati dei componenti utilizzando una libreria di stati come NgRx.
* **Opzione 3:** Sfrutta la gerarchia degli oggetti personalizzando ed estendendo il componente contenitore .

## Passaggi successivi {#next-steps}

Per una guida dettagliata alla creazione di un tuo SPA, consulta la sezione [Guida introduttiva all’editor di SPA AEM - Tutorial eventi WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=it).

Per ulteriori informazioni su come organizzarsi per sviluppare SPA per AEM vedere l&#39;articolo [Sviluppo di SPA per AEM](/help/sites-developing/spa-architecture.md).

Per ulteriori dettagli sul modello dinamico per la mappatura dei componenti e su come funziona all’interno di SPA in AEM, consulta l’articolo [Mappatura dinamica da modello a componente per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desideri implementare SPA in AEM per un framework diverso da React o Angular o desideri semplicemente approfondire il funzionamento dell’SDK SPA per AEM, consulta [Blueprint SPA](/help/sites-developing/spa-blueprint.md) articolo.
