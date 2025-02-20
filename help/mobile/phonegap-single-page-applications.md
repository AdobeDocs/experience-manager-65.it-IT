---
title: Applicazioni a pagina singola
description: Segui questa pagina per scoprire di più sulle applicazioni a pagina singola, ovvero puoi creare un’applicazione che funziona in modo identico a un’applicazione desktop o mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# Applicazioni a pagina singola{#single-page-applications}

{{ue-over-mobile}}

[Le applicazioni a pagina singola](https://en.wikipedia.org/wiki/Single-page_application) (SPA) hanno raggiunto la massa critica, ampiamente considerate come il modello più efficace per creare esperienze senza soluzione di continuità con la tecnologia Web. Seguendo un modello SPA, puoi creare un’applicazione che funziona in modo identico a un’app desktop o mobile, ma che raggiunge una moltitudine di piattaforme per dispositivi e fattori di forma grazie alle sue basi negli standard web aperti.

In generale, l&#39;SPA appare più performante dei siti web tradizionali basati su pagina perché in genere caricano una pagina HTML completa **una sola** (inclusi CSS, JS e il contenuto font di supporto), e quindi caricano solo ciò che è necessario ogni volta che si verifica un cambiamento di stato nell&#39;app. Ciò che è necessario per questo cambiamento di stato può variare in base al set di tecnologie scelte, ma in genere include un singolo frammento HTML per sostituire la &quot;visualizzazione&quot; esistente e l’esecuzione di un blocco di codice JS per collegare la nuova visualizzazione ed eseguire qualsiasi rendering di modelli lato client che potrebbe essere necessario. La velocità di questo cambiamento di stato può essere ulteriormente migliorata supportando i meccanismi di caching dei modelli o anche l’accesso offline al contenuto dei modelli se si utilizza Adobe PhoneGap.

L&#39;AEM 6.1 sostiene la creazione e la gestione dell&#39;SPA tramite le app per l&#39;AEM. Questo articolo fornisce un&#39;introduzione ai concetti alla base dell&#39;SPA e al modo in cui utilizzano [AngularJS](https://angularjs.org/) per portare il tuo marchio in App Store e Google Play.

## SPA nelle applicazioni AEM {#spa-in-aem-apps}

Il framework delle applicazioni a pagina singola nelle app AEM consente di ottenere prestazioni elevate da un’app AngularJS, consentendo agli autori (o ad altro personale non tecnico) di creare e gestire i contenuti dell’app tramite l’ambiente di editor drag-and-drop ottimizzato per il tocco, tradizionalmente riservato alla gestione dei siti web. Hai già un sito costruito con l&#39;AEM? Con le app AEM puoi riutilizzare facilmente contenuti, componenti, flussi di lavoro, risorse e autorizzazioni.

## Modulo applicativo AngularJS {#angularjs-application-module}

Le app AEM gestiscono gran parte della configurazione AngularJS, inclusa la creazione del modulo di livello superiore dell’app. Per impostazione predefinita, questo modulo è denominato &quot;AEMAngularApp&quot; e lo script responsabile della sua generazione è reperibile (e sovrapposto) in /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte dell’inizializzazione dell’app consiste nello specificare da quali moduli AngularJS dipende l’app. L’elenco dei moduli utilizzati dall’app è specificato da uno script che si trova in /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp e può essere sovrapposto dal componente pagina delle tue app per richiamare eventuali moduli AngularJS aggiuntivi richiesti dall’app. Ad esempio, confronta lo script precedente con l’implementazione Geometrixx (che si trova in /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Per supportare la navigazione tra gli stati distinti nell’app, lo script del modulo angular-app scorre tutte le pagine discendenti della pagina dell’app principale per generare un set di &quot;route&quot; e configura ogni percorso nel servizio $routeProvider di Angular. Ad esempio, osserva lo script del modulo angular-app generato dall&#39;app di Geometrixx Outdoors: (il collegamento richiede un&#39;istanza locale) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Accedendo all’app AEMAngularApp generata, trovi una serie di route specificate come segue:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

L&#39;esempio precedente illustra in particolare un esempio di passaggio di un parametro come parte del percorso. In questo esempio, indica che quando viene richiesto un percorso che soddisfa il modello specificato (/content/phonegap/geometrixx-outdoors/en/home/products/:id), deve essere gestito dal modello home/products.template.html e utilizzare il controller &quot;contentphonegapgeometrixxoutdoorsenhomeproducts&quot;.

Il modello da caricare quando viene richiesta questa route è specificato dalla proprietà templateUrl. Questo modello contiene i HTML dei componenti AEM inclusi nella pagina e tutte le direttive AngularJS necessarie per collegare il lato client dell’applicazione. Per un esempio di direttiva AngularJS in un componente Geometrixx, consulta la riga 45 del file template.jsp del pannello di scorrimento (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Controller di pagina {#page-controllers}

Nelle stesse parole di Angular, &quot;un controller è una funzione di costruzione di JavaScript utilizzata per potenziare l&#39;ambito dell&#39;Angular&quot;. ([source](https://docs.angularjs.org/guide/controller)) Ogni pagina in un&#39;app AEM viene collegata automaticamente a un controller che può essere potenziato da qualsiasi controller che specifica un `frameworkType` di `angular`. Osserva il componente ng-text come esempio (/libs/mobileapps/components/angular/ng-text), incluso il nodo cq:template che si assicura che ogni volta che questo componente viene aggiunto a una pagina, includa questa importante proprietà.

Per un esempio più complesso di controller, apri lo script ng-template-page controller.jsp (in /apps/geometrixx-outdoors-app/components/angular/ng-template-page). Di particolare interesse è il codice JavaScript generato al momento dell’esecuzione, che esegue il rendering come segue:

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

Nell&#39;esempio precedente, il parametro del servizio `$routeParams` viene preso e quindi massaggiato nella struttura di directory in cui sono memorizzati i dati JSON. Gestendo lo SKU `id` in questo modo, è possibile fornire un unico modello di prodotto in grado di eseguire il rendering dei dati del prodotto per migliaia di prodotti potenzialmente distinti. Si tratta di un modello molto più scalabile che richiede un percorso individuale per ogni elemento in un database di prodotti (potenzialmente) di grandi dimensioni.

Ci sono anche due componenti in azione qui: ng-product potenzia l&#39;ambito con i dati estratti dalla chiamata `$http` precedente. In questa pagina è inoltre presente un&#39;immagine ng che a sua volta potenzia l&#39;ambito con il valore che recupera dalla risposta. In virtù del servizio `$http` di Angular, ogni componente attende pazientemente il completamento della richiesta e il completamento della promessa creata.

## Passaggi successivi {#the-next-steps}

Dopo aver appreso le applicazioni a pagina singola, consulta [Sviluppo di app con PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md).
