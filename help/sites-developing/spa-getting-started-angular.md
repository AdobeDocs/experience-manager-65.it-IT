---
title: Guida introduttiva alle app SPA in AEM - Angular
seo-title: Guida introduttiva alle app SPA in AEM - Angular
description: Questo articolo presenta un'applicazione SPA di esempio, spiega come viene assemblata e consente di iniziare a utilizzare rapidamente la propria SPA utilizzando il framework Angular.
seo-description: Questo articolo presenta un'applicazione SPA di esempio, spiega come viene assemblata e consente di iniziare a utilizzare rapidamente la propria SPA utilizzando il framework Angular.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 1%

---


# Guida introduttiva alle app SPA in AEM - Angular{#getting-started-with-spas-in-aem-angular}

Le applicazioni SPA (Single Page Applications) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando i framework SPA e gli autori desiderano modificare i contenuti all&#39;interno AEM per un sito creato utilizzando i framework SPA.

La funzione di authoring SPA offre una soluzione completa per supportare gli SPA in AEM. Questo articolo presenta un&#39;applicazione SPA semplificata sul framework Angular, spiega come viene assemblato, consentendo di iniziare rapidamente a utilizzare la propria SPA.

>[!NOTE]
>
>Questo articolo si basa sulla cornice angolare. Per il documento corrispondente per il framework React, consulta [Guida introduttiva alle app AEM - React](/help/sites-developing/spa-getting-started-react.md).

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono il rendering lato client basato su SPA (ad esempio React o Angular).

## Introduzione {#introduction}

Questo articolo riassume il funzionamento di base di una semplice SPA e il minimo che devi sapere per far funzionare il tuo.

Per maggiori dettagli sul funzionamento degli SPA in AEM, consulta i documenti seguenti:

* [Introduzione e introduzione SPA](/help/sites-developing/spa-walkthrough.md)
* [Introduzione all&#39;authoring SPA](/help/sites-developing/spa-overview.md)
* [Blueprint SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Per poter creare contenuti all’interno di un’app SPA, questi devono essere memorizzati in AEM ed essere esposti dal modello di contenuto.
>
>Una SPA sviluppata al di fuori di AEM non sarà autorizzata se non rispetta il contratto per i modelli di contenuto.

Questo documento illustra la struttura di un&#39;app SPA semplificata e illustra il suo funzionamento, in modo da poter applicare questa comprensione all&#39;app SPA.

## Dipendenze, configurazione e generazione {#dependencies-configuration-and-building}

Oltre alla dipendenza Angular prevista, il campione SPA può sfruttare librerie aggiuntive per rendere più efficiente la creazione dell&#39;SPA.

### Dipendenze {#dependencies}

Il `package.json` file definisce i requisiti del pacchetto SPA complessivo. Le dipendenze AEM minime richieste sono elencate di seguito.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

La funzione `aem-clientlib-generator` viene utilizzata per rendere automatica la creazione di librerie client nel processo di creazione.

`"aem-clientlib-generator": "^1.4.1",`

Maggiori dettagli sono disponibili [su GitHub qui](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versione minima della `aem-clientlib-generator` richiesta è 1.4.1.

Il file `aem-clientlib-generator` è configurato nel `clientlib.config.js` modo seguente.

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

In realtà, la creazione dell&#39;app si basa su [Webpack](https://webpack.js.org/) per la traslazione oltre al generatore aem-clientlib-generator per la creazione automatica della libreria client. Il comando build sarà quindi simile a:

`"build": "ng build --build-optimizer=false && clientlib",`

Una volta creato, il pacchetto può essere caricato in un&#39;istanza AEM.

### AEM Project Archetype {#aem-project-archetype}

Qualsiasi progetto AEM dovrebbe sfruttare il [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta i progetti SPA utilizzando React o Angular e sfrutta l’SDK SPA.

## Struttura dell&#39;applicazione {#application-structure}

L&#39;inclusione delle dipendenze e la creazione dell&#39;app come descritto in precedenza vi lasceranno con un pacchetto SPA funzionante che potete caricare nell&#39;istanza AEM.

La sezione successiva di questo documento illustra la struttura di un&#39;app in AEM, i file importanti che guidano l&#39;applicazione e il modo in cui lavorano insieme.

Un componente immagine semplificato viene utilizzato come esempio, ma tutti i componenti dell’applicazione si basano sullo stesso concetto.

### app.module.ts {#app-module-ts}

Il punto di ingresso nell&#39;SPA è il `app.module.ts` file mostrato qui semplificato per concentrarsi sul contenuto importante.

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

Il `app.module.ts` file è il punto di partenza dell&#39;app e contiene la configurazione di progetto iniziale e viene utilizzato `AppComponent` per avviare l&#39;app.

#### Istanziazione statica {#static-instantiation}

Quando un’istanza del componente viene creata in modo statico utilizzando il modello di componente, il valore deve essere passato dal modello alle proprietà del componente. I valori del modello vengono passati come attributi per essere successivamente disponibili come proprietà del componente.

### app.component.ts {#app-component-ts}

Una volta `app.module.ts` avviati `AppComponent`, l&#39;app può quindi essere inizializzata, come illustrato in una versione semplificata per concentrarsi sul contenuto importante.

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

Elaborando la pagina, `app.component.ts` le chiamate `main-content.component.ts` elencate in questa sezione vengono semplificate.

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

Consente di `MainComponent` acquisire la rappresentazione JSON del modello di pagina ed elaborare il contenuto da racchiudere/decorare ogni elemento della pagina. Per maggiori informazioni, `Page` consulta il documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

Il componente `Page` è composto da componenti. Con l’assimilazione del JSON, il gruppo `Page` può elaborare tali componenti, come `image.component.ts` illustrato di seguito.

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

L&#39;idea centrale di SPA in AEM è la mappatura dei componenti SPA ai componenti AEM e l&#39;aggiornamento del componente quando il contenuto viene modificato (e viceversa). Per un riepilogo di questo modello di comunicazione, consulta Panoramica [sull’editor](/help/sites-developing/spa-overview.md) SPA.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

Il `MapTo` metodo mappa il componente SPA sul componente AEM. Supporta l&#39;uso di una singola stringa o di una matrice di stringhe.

`ImageEditConfig` è un oggetto di configurazione che contribuisce a abilitare le funzionalità di authoring di un componente fornendo i metadati necessari affinché l’editor generi i segnaposto

In assenza di contenuto, le etichette vengono fornite come segnaposto per rappresentare il contenuto vuoto.

#### Proprietà trasmesse dinamicamente {#dynamically-passed-properties}

I dati provenienti dal modello vengono passati in modo dinamico come proprietà del componente.

### image.component.html {#image-component-html}

Infine, l’immagine può essere riprodotta in `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Condivisione delle informazioni tra i componenti SPA {#sharing-information-between-spa-components}

È necessario che i componenti all’interno di un’applicazione a pagina singola condividano informazioni. Ci sono diversi modi consigliati di fare questo, elencati come segue in ordine crescente di complessità.

* **Opzione 1:** Centralizzate la logica e la trasmissione ai componenti necessari, ad esempio utilizzando una classe util come soluzione orientata agli oggetti.
* **Opzione 2:** Condividere gli stati dei componenti utilizzando una libreria di stati come NgRx.
* **Opzione 3:** Sfruttare la gerarchia di oggetti personalizzando ed estendendo il componente contenitore.

## Passaggi successivi {#next-steps}

Per una guida passo-passo alla creazione di un vostro SPA, consultate la [Guida introduttiva all’editor SPA AEM - Esercitazione](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)sugli eventi WKND.

Per ulteriori informazioni su come organizzarsi per sviluppare SPA per AEM vedere l&#39;articolo [Sviluppo di SPA per AEM](/help/sites-developing/spa-architecture.md).

Per ulteriori dettagli sulla mappatura del modello dinamico a componente e sul suo funzionamento all&#39;interno degli SPA in AEM, consultate l&#39;articolo Mappatura [dinamica da modello a componente per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desideri implementare gli SPA in AEM per un framework diverso da React o Angular o vuoi semplicemente approfondire il funzionamento dell’SDK SPA per AEM, consulta l’articolo [SPA Blueprint](/help/sites-developing/spa-blueprint.md) .
