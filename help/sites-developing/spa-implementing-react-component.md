---
title: Implementazione di un Componente React per applicazioni a pagina singola (SPA)
description: Questo articolo illustra come adattare un componente React semplice esistente all’editor SPA di Adobe Experience Manager (AEM).
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 9%

---

# Implementazione di un Componente React per applicazioni a pagina singola (SPA){#implementing-a-react-component-for-spa}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando framework SPA e gli autori desiderano modificare facilmente i contenuti all’interno di Adobe Experience Manager (AEM) per un sito creato utilizzando framework SPA.

La funzione di authoring dell’SPA offre una soluzione completa per il supporto dell’SPA nell’ambito dell’AEM. Questo articolo presenta un esempio di come adattare un componente React semplice ed esistente per lavorare con l’Editor SPA dell’AEM.

>[!NOTE]
>
>L’editor SPA è la soluzione consigliata per i progetti che richiedono il rendering lato client basato sul framework SPA (ad esempio, React o Angular).

## Introduzione {#introduction}

Grazie al contratto semplice e leggero richiesto dall&#39;AEM e stabilito tra l&#39;SPA e l&#39;SPA Editor, è facile prendere un&#39;applicazione JavaScript esistente e adattarla per l&#39;uso con un SPA in AEM.

Questo articolo illustra l’esempio della componente meteo sull’SPA di esempio del Diario We.Retail.

Prima di leggere questo articolo, è necessario conoscere la struttura [di un&#39;applicazione SPA per AEM](/help/sites-developing/spa-getting-started-react.md).

>[!CAUTION]
>In questo documento viene utilizzata l&#39;app [We.Retail Journal](https://github.com/adobe/aem-sample-we-retail-journal) solo a scopo dimostrativo. Non utilizzarlo per alcun lavoro di progetto.
>
>Qualsiasi progetto AEM deve utilizzare l’[archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Componente meteo {#the-weather-component}

Il componente meteo si trova in alto a sinistra nell’app We.Retail Journal. Visualizza il meteo corrente di una posizione definita, estraendo i dati meteo in modo dinamico.

### Utilizzo del widget meteo {#using-the-weather-widget}

![schermata_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

Quando si crea un contenuto dell’SPA nell’Editor SPA, la componente meteo viene visualizzata come qualsiasi altro componente AEM, completa di una barra degli strumenti, ed è modificabile.

![schermata_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

La città può essere aggiornata in una finestra di dialogo come qualsiasi altra componente dell’AEM.

![schermata_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

La modifica viene mantenuta e il componente si aggiorna automaticamente con i nuovi dati meteo.

![schermata_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementazione componente meteo {#weather-component-implementation}

La componente meteo si basa su un componente React disponibile pubblicamente, denominato [React Open Weather](https://www.npmjs.com/package/react-open-weather). È stato adattato per funzionare come componente nell’applicazione SPA di esempio di We.Retail Journal.

Di seguito sono riportati alcuni snippet della documentazione NPM relativa all’utilizzo del componente React Open Weather.

![schermata_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![schermata_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Analisi del codice del componente meteo personalizzato ( `Weather.js`) nell&#39;applicazione del diario We.Retail:

* **Riga 16**: il widget Meteo React Open è stato caricato come richiesto.
* **Riga 46**: la funzione `MapTo` collega il componente React a un componente AEM corrispondente in modo che possa essere modificato nell&#39;editor SPA.

* **Righe 22-29**: `EditConfig` è definito, verificando se la città è stata popolata e definendo il valore se vuoto.

* **Righe 31-44**: il componente Meteo estende la classe `Component` e fornisce i dati richiesti come definito nella documentazione di utilizzo NPM per il componente Meteo aperto di React ed esegue il rendering del componente.

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

Anche se un componente back-end deve già esistere, lo sviluppatore front-end può utilizzare il componente React Open Weather nell’SPA di We.Retail Journal con poca codifica.

## Passaggio successivo {#next-step}

Per ulteriori informazioni sullo sviluppo dell&#39;SPA per l&#39;AEM, vedere l&#39;articolo [Sviluppo dell&#39;SPA per l&#39;AEM](/help/sites-developing/spa-architecture.md).
