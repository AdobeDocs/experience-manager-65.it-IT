---
title: Implementazione di un Componente React per applicazioni a pagina singola (SPA)
seo-title: Implementing a React Component for SPA
description: Questo articolo presenta un esempio di come adattare un semplice componente React esistente per lavorare con l’editor di SPA di AEM.
seo-description: This article presents an example of how to adapt a simple, existing React component to work with the AEM SPA Editor.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 6%

---

# Implementazione di un Componente React per applicazioni a pagina singola (SPA){#implementing-a-react-component-for-spa}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano poter creare siti utilizzando framework SPA e gli autori desiderano modificare i contenuti all’interno di AEM per un sito creato utilizzando framework SPA.

La funzione di authoring SPA offre una soluzione completa per supportare SPA all’interno di AEM. Questo articolo presenta un esempio di come adattare un semplice componente React esistente per lavorare con l’editor di SPA di AEM.

>[!NOTE]
>
>L’editor di SPA è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad esempio, React o Angular).

## Introduzione {#introduction}

Grazie al contratto semplice e leggero richiesto da AEM e stabilito tra il SPA e l&#39;editor SPA, prendere un&#39;applicazione Javascript esistente e adattarla per l&#39;uso con un SPA in AEM è una questione semplice.

Questo articolo illustra l’esempio del componente meteo nel SPA di esempio di We.Retail Journal.

Devi acquisire familiarità con le [struttura di una domanda SPA di AEM](/help/sites-developing/spa-getting-started-react.md) prima di leggere questo articolo.

>[!CAUTION]
>Questo documento utilizza [App Journal We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) solo a scopo dimostrativo. Non deve essere utilizzato per alcun lavoro di progetto.
>
>Qualsiasi progetto AEM deve sfruttare [Archetipo di progetto AEM](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/developing/archetype/overview.html), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Componente meteo {#the-weather-component}

Il componente meteo si trova in alto a sinistra nell’app We.Retail Journal. Mostra il tempo corrente di una posizione definita, estraendo dinamicamente i dati meteo.

### Utilizzo del Widget meteo {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

Quando si creano contenuti del SPA nell’Editor SPA, il componente meteo viene visualizzato come qualsiasi altro componente AEM, completo di una barra degli strumenti, ed è modificabile.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

La città può essere aggiornata in una finestra di dialogo come qualsiasi altro componente AEM.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

Il cambiamento viene mantenuto e il componente si aggiorna automaticamente con i nuovi dati meteo.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementazione del componente meteo {#weather-component-implementation}

La componente Tempo è in realtà basata su una componente React disponibile al pubblico, chiamata [React Open Weather](https://www.npmjs.com/package/react-open-weather), che è stato adattato per funzionare come componente all’interno dell’applicazione di esempio SPA Journal We.Retail.

Di seguito sono riportati alcuni snippet della documentazione NPM sull’utilizzo del componente React Open Weather.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Revisione del codice del componente meteo personalizzato ( `Weather.js`) nell&#39;applicazione We.Retail Journal:

* **Linea 16**: Il widget React Open Weather viene caricato come necessario.
* **Linea 46**: La `MapTo` La funzione relaziona questo componente React a un componente AEM corrispondente in modo che possa essere modificato nell&#39;editor di SPA.

* **Linee 22-29**: La `EditConfig` è definito, controllando se la città è stata compilata e definendo il valore se vuoto.

* **Linee 31-44**: Il componente Tempo estende la `Component` e fornisce i dati richiesti come definito nella documentazione sull&#39;utilizzo di NPM per il componente React Open Weather ed esegue il rendering del componente.

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

Anche se un componente back-end deve già esistere, lo sviluppatore front-end può sfruttare il componente React Open Weather nel SPA We.Retail Journal con una codifica molto ridotta.

## Passaggio successivo {#next-step}

Per ulteriori informazioni sullo sviluppo di SPA per AEM vedi l&#39;articolo [Sviluppo di SPA per AEM](/help/sites-developing/spa-architecture.md).
