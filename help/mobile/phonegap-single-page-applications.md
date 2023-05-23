---
title: Applicazioni a pagina singola
seo-title: Single Page Applications
description: Segui questa pagina per scoprire di più sulle applicazioni a pagina singola, ovvero puoi creare un’applicazione che funziona in modo identico a un’applicazione desktop o mobile.
seo-description: Follow this page to learn about single page applications, that is, you can create an application that performs identically to a desktop or mobile application.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 1%

---

# Applicazioni a pagina singola{#single-page-applications}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

[Applicazioni a pagina singola](https://en.wikipedia.org/wiki/Single-page_application) (SPA) hanno raggiunto una massa critica, ampiamente considerata come lo schema più efficace per creare esperienze senza soluzione di continuità con la tecnologia web. Seguendo un modello SPA, puoi creare un’applicazione che funziona in modo identico a un’app desktop o mobile, ma che raggiunge una moltitudine di piattaforme per dispositivi e fattori di forma grazie alle sue basi negli standard web aperti.

In generale, l’SPA sembra più performante dei siti web tradizionali basati su pagine, in quanto generalmente caricano una pagina HTML completa **una sola volta** (inclusi CSS, JS e il contenuto dei caratteri di supporto), quindi carica solo ciò che è esattamente necessario ogni volta che si verifica un cambiamento di stato nell’app. Ciò che è necessario per questo cambiamento di stato può variare in base al set di tecnologie scelte, ma in genere include un singolo frammento HTML per sostituire la &quot;visualizzazione&quot; esistente e l’esecuzione di un blocco di codice JS per collegare la nuova visualizzazione ed eseguire qualsiasi rendering di modelli lato client che potrebbe essere necessario. La velocità di questo cambiamento di stato può essere ulteriormente migliorata supportando i meccanismi di caching dei modelli o anche l’accesso offline al contenuto dei modelli se si utilizza Adobe PhoneGap.

L&#39;AEM 6.1 sostiene la creazione e la gestione dell&#39;SPA tramite le app per l&#39;AEM. Questo articolo fornisce un’introduzione ai concetti alla base del SPA e al modo in cui essi sfruttano [AngularJS](https://angularjs.org/) per portare il tuo marchio su App Store e Google Play.

## SPA nelle applicazioni AEM {#spa-in-aem-apps}

Il framework delle applicazioni a pagina singola nelle app AEM consente di ottenere prestazioni elevate da un’app AngularJS, consentendo agli autori (o ad altro personale non tecnico) di creare e gestire i contenuti dell’app tramite l’ambiente di editor drag-and-drop ottimizzato per il tocco, tradizionalmente riservato alla gestione dei siti web. Hai già un sito costruito con l&#39;AEM? Il riutilizzo di contenuti, componenti, flussi di lavoro, risorse e autorizzazioni è molto semplice con le app AEM.

## Modulo applicativo AngularJS {#angularjs-application-module}

Le app AEM gestiscono gran parte della configurazione AngularJS, inclusa la creazione del modulo di livello superiore dell’app. Per impostazione predefinita, questo modulo è denominato &quot;AEMAngularApp&quot; e lo script responsabile della sua generazione è disponibile (e sovrapposto) all’indirizzo /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte dell’inizializzazione dell’app consiste nello specificare da quali moduli AngularJS dipende l’app. L’elenco dei moduli utilizzati dall’app è specificato da uno script che si trova in /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp e può essere sovrapposto dal componente pagina delle tue app per richiamare eventuali moduli AngularJS aggiuntivi richiesti dall’app. Ad esempio, confronta lo script precedente con l’implementazione Geometrixx (che si trova in /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Per supportare la navigazione tra gli stati distinti nell’app, lo script del modulo angular-app scorre tutte le pagine discendenti della pagina dell’app di livello superiore per generare un set di &quot;route&quot; e configura ogni percorso nel servizio $routeProvider di Angular. Ad esempio, osserva lo script di modulo angular-app generato dall’app Geometrixx Outdoors: (il collegamento richiede un’istanza locale) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Accedendo all’app AEMAngularApp generata, troverai una serie di route specificate come segue:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

L&#39;esempio precedente illustra in particolare un esempio di passaggio di un parametro come parte del percorso. In questo esempio si indica che quando viene richiesto un percorso che soddisfa il pattern specificato (/content/phonegap/geometrixx-outdoors/en/home/products/:id), questo deve essere gestito dal modello home/products.template.html e utilizzare il controller &quot;contentphonegapgeometrixxoutdoorsenhomeproducts&quot;.

Il modello da caricare quando viene richiesta questa route è specificato dalla proprietà templateUrl. Questo modello conterrà i HTML dei componenti AEM inclusi nella pagina, nonché tutte le direttive AngularJS necessarie per collegare il lato client dell’applicazione. Ad esempio, una direttiva AngularJS in un componente Geometrixx, osserva la riga 45 del file template.jsp del carosello di scorrimento (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Controller di pagina {#page-controllers}

Nelle stesse parole di Angular, &quot;un controller è una funzione di costruzione JavaScript utilizzata per potenziare l’ambito Angular&quot;. ([sorgente](https://docs.angularjs.org/guide/controller)a) Ogni pagina di un&#39;app AEM viene collegata automaticamente a un controller che può essere potenziato da qualsiasi controller che specifichi `frameworkType` di `angular`. Osserva il componente ng-text come esempio (/libs/mobileapps/components/angular/ng-text), incluso il nodo cq:template che si assicura che ogni volta che questo componente viene aggiunto a una pagina, includa questa importante proprietà.

Per un esempio più complesso di controller, apri lo script ng-template-page controller.jsp (che si trova in /apps/geometrixx-outdoors-app/components/angular/ng-template-page). Di particolare interesse è il codice JavaScript generato quando viene eseguito, che esegue il rendering come segue:

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

Nell’esempio precedente, noterai che stiamo prendendo un parametro dal `$routeParams` e quindi massaggiarlo nella struttura di directory in cui sono memorizzati i nostri dati JSON. Trattando con lo SKU `id` in questo modo, siamo in grado di fornire un singolo modello di prodotto che può eseguire il rendering dei dati di prodotto per potenzialmente migliaia di prodotti distinti. Si tratta di un modello molto più scalabile che richiede un percorso individuale per ogni elemento in un database di prodotti (potenzialmente) di grandi dimensioni.

Sono inoltre disponibili due componenti: ng-product potenzia l’ambito con i dati estratti dal precedente `$http` chiamare. In questa pagina è inoltre presente un&#39;immagine ng che a sua volta potenzia l&#39;ambito con il valore che recupera dalla risposta. In virtù dell&#39;Angular `$http` ogni componente attende pazientemente il completamento della richiesta e il completamento della promessa creata.

## Passaggi successivi {#the-next-steps}

Dopo aver appreso le applicazioni a pagina singola, consulta [Sviluppo di app con PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md).
