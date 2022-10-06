---
title: Applicazioni a pagina singola
seo-title: Single Page Applications
description: Segui questa pagina per scoprire le applicazioni a pagina singola, ovvero puoi creare un'applicazione che funziona in modo identico per un'applicazione desktop o mobile.
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
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

[Applicazioni a pagina singola](https://en.wikipedia.org/wiki/Single-page_application) (SPA) hanno raggiunto la massa critica, ampiamente considerata come il modello più efficace per creare esperienze senza soluzione di continuità con la tecnologia web. Seguendo un pattern di SPA, è possibile creare un’applicazione che esegue in modo identico un’applicazione desktop o mobile, ma che raggiunge una moltitudine di piattaforme di dispositivi e fattori di forma a causa della sua base in standard web aperti.

In generale, SPA appaiono più performanti dei siti web tradizionali basati su pagine, in quanto generalmente caricano una pagina HTML completa **una volta** (inclusi CSS, JS e il contenuto dei font di supporto) e quindi carica solo esattamente ciò che è necessario ogni volta che nell’app si verifica una modifica dello stato. Ciò che è necessario per questo cambiamento di stato può variare in base al set di tecnologie scelte, ma in genere include un singolo frammento di HTML per sostituire la &quot;vista&quot; esistente e l’esecuzione di un blocco di codice JS per collegare la nuova visualizzazione ed eseguire qualsiasi rendering del modello lato client che potrebbe essere necessario. La velocità di questa modifica dello stato può essere ulteriormente migliorata supportando i meccanismi di memorizzazione nella cache dei modelli o persino l&#39;accesso offline al contenuto del modello se si utilizza Adobe PhoneGap.

AEM 6.1 sostiene la costruzione e la gestione di SPA tramite AEM Apps. Questo articolo fornisce un&#39;introduzione ai concetti alla base del SPA e come essi sfruttano [AngularJS](https://angularjs.org/) per portare il tuo marchio su App Store e Google Play.

## SPA nelle app AEM {#spa-in-aem-apps}

Il framework di applicazione a pagina singola nelle app di AEM consente di ottenere prestazioni elevate in un’app AngularJS, consentendo agli autori (o altro personale non tecnico) di creare e gestire il contenuto dell’app tramite l’ambiente di editor touch e con trascinamento tradizionalmente riservato alla gestione dei siti web. Hai già creato un sito con AEM? Scoprirai che riutilizzare i contenuti, i componenti, i flussi di lavoro, le risorse e le autorizzazioni è facile con le app AEM.

## Modulo applicazione AngularJS {#angularjs-application-module}

AEM Apps gestisce gran parte della configurazione di AngularJS per te, inclusa la configurazione del modulo di livello superiore dell&#39;app. Per impostazione predefinita questo modulo si chiama &quot;AEMAngularApp&quot; e lo script responsabile della sua generazione si trova (e sovrapposto) all’indirizzo /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte dell&#39;inizializzazione dell&#39;app prevede la specifica dei moduli AngularJS da cui dipende l&#39;app. L’elenco dei moduli utilizzati dall’app è specificato da uno script situato in /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp e può essere sovrapposto dal componente page delle tue app per richiamare eventuali moduli AngularJS aggiuntivi richiesti dall’app. Ad esempio, confronta lo script precedente con l’implementazione di Geometrixx (che si trova all’indirizzo /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Per supportare la navigazione tra gli stati distinti nell’app, lo script del modulo angular-app-module esegue un’iterazione tra tutte le pagine discendenti della pagina dell’app di livello principale per generare un set di &quot;route&quot; e configura ogni percorso nel servizio $routeProvider di Angular. Per un esempio di come si presenta in pratica, osserva lo script modulo-app-angular generato dall’app Geometrixx Outdoors: (il collegamento richiede un&#39;istanza locale) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Effettuando l’accesso a AEMAngularApp generata, troverai una serie di percorsi specificati come segue:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

L&#39;esempio precedente illustra in particolare un esempio di passaggio di un parametro come parte del percorso. In questo esempio stiamo indicando che quando un percorso che soddisfa il pattern specificato (/content/phonegap/geometrixx-outdoors/en/home/products/:id) è richiesto, deve essere gestito dal modello home/products.template.html e utilizzare il controller &#39;contentphonegapgeometrixxoutdoorsenhomeproducts&#39;.

Il modello da caricare quando si richiede questa route è specificato dalla proprietà templateUrl . Questo modello conterrà il HTML da AEM componenti inclusi nella pagina, nonché tutte le direttive AngularJS necessarie per il cablaggio del lato client dell’applicazione. Per un esempio di direttiva AngularJS in un componente Geometrixx, osserva la riga 45 del template.jsp di swipe-carosello (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Titolari del trattamento delle pagine {#page-controllers}

Nelle parole proprie dell&#39;Angular, &quot;un controller è una funzione di costruzione JavaScript utilizzata per potenziare l&#39;ambito dell&#39;Angular.&quot; ([source](https://docs.angularjs.org/guide/controller)) Ogni pagina di un&#39;app AEM è collegata automaticamente a un controller che può essere incrementato da qualsiasi controller che specifica un `frameworkType` di `angular`. Osserva il componente ng-text come un esempio (/libs/mobileapps/components/angular/ng-text), incluso il nodo cq:template che assicura che ogni volta che questo componente viene aggiunto a una pagina includa questa importante proprietà.

Per un esempio di controller più complesso, apri lo script ng-template-page controller.jsp (che si trova in /apps/geometrixx-outdoors-app/components/angular/ng-template-page). Di particolare interesse è il codice javascript generato quando eseguito, che esegue il rendering come segue:

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

Nell’esempio precedente, noterai che stiamo prendendo un parametro dal `$routeParams` e poi massaggiarlo nella struttura di directory in cui sono memorizzati i nostri dati JSON. Trattando lo sku `id` in questo modo, siamo in grado di fornire un singolo modello di prodotto che può eseguire il rendering dei dati del prodotto per migliaia di prodotti distinti potenzialmente. Si tratta di un modello molto più scalabile che richiede un percorso individuale per ogni elemento in un database di prodotti di massa (potenzialmente).

Ci sono anche due componenti al lavoro qui: ng-product aumenta l&#39;ambito di applicazione con i dati estratti da quanto sopra `$http` chiama. C&#39;è anche un&#39;immagine ng in questa pagina che a sua volta aumenta anche l&#39;ambito con il valore che recupera dalla risposta. In virtù del Angular `$http` ogni componente aspetterà pazientemente finché la richiesta non viene completata e la promessa creata viene soddisfatta.

## Passaggi successivi {#the-next-steps}

Dopo aver appreso le applicazioni a pagina singola, vedi [Sviluppo di app con PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md).
