---
title: Applicazioni a pagina singola
seo-title: Applicazioni a pagina singola
description: Seguite questa pagina per informazioni sulle applicazioni a pagina singola, ovvero potete creare un'applicazione che esegue in modo identico a un'applicazione desktop o mobile.
seo-description: Seguite questa pagina per informazioni sulle applicazioni a pagina singola, ovvero potete creare un'applicazione che esegue in modo identico a un'applicazione desktop o mobile.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Applicazioni a pagina singola{#single-page-applications}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

[Le applicazioni](https://en.wikipedia.org/wiki/Single-page_application) SPA (Single Page Applications) hanno raggiunto una massa critica, ampiamente considerata come il modello più efficace per creare esperienze perfette con la tecnologia Web. Seguendo un pattern SPA, è possibile creare un&#39;applicazione che funziona in modo identico a un&#39;applicazione desktop o mobile, ma che raggiunge un gran numero di piattaforme di dispositivi e di fattori di forma a causa del suo fondamento in standard Web aperti.

In generale, gli SPA appaiono più efficaci dei siti Web basati sulle pagine tradizionali, perché in genere caricano una pagina HTML completa **solo una volta** (inclusi CSS, JS e contenuti di supporto per i font), quindi caricano solo ciò che è necessario ogni volta che si verifica una modifica di stato nell&#39;app. Ciò che è necessario per questa modifica di stato può variare in base al set di tecnologie selezionate, ma in genere include un singolo frammento HTML per sostituire la &quot;vista&quot; esistente, e l&#39;esecuzione di un blocco di codice JS per collegare la nuova vista ed eseguire il rendering di modelli lato client che potrebbe essere necessario. La velocità di questa modifica dello stato può essere ulteriormente migliorata grazie al supporto dei meccanismi di memorizzazione nella cache dei modelli, o anche tramite l&#39;accesso offline ai contenuti dei modelli se si utilizza Adobe PhoneGap.

AEM 6.1 supporta la creazione e la gestione di app SPA tramite AEM Apps. Questo articolo fornisce un&#39;introduzione ai concetti alla base dell&#39;SPA e come sfruttano [AngularJS](https://angularjs.org/) per portare il tuo marchio nell&#39;App Store e in Google Play.

## SPA nelle app AEM {#spa-in-aem-apps}

Il framework di applicazione per pagina singola nelle app AEM consente di ottenere prestazioni elevate per un&#39;app AngularJS, consentendo agli autori (o ad altro personale non tecnico) di creare e gestire il contenuto dell&#39;app tramite l&#39;editor touch, tradizionalmente riservato alla gestione di siti Web. È già stato creato un sito con AEM? Le app AEM semplificano il riutilizzo di contenuti, componenti, flussi di lavoro, risorse e autorizzazioni.

## Modulo applicazione AngularJS {#angularjs-application-module}

Le app AEM gestiscono gran parte della configurazione AngularJS per voi, inclusa la configurazione del modulo di livello principale dell&#39;app. Per impostazione predefinita, questo modulo è denominato &#39;AEMAngularApp&#39; e lo script responsabile della generazione del modulo è disponibile (e sovrapposto) all&#39;indirizzo /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte dell&#39;inizializzazione dell&#39;app prevede la specifica dei moduli AngularJS da cui dipende l&#39;app. L&#39;elenco dei moduli utilizzati dall&#39;app è specificato da uno script ubicato in /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp e può essere sovrapposto dal componente pagina delle app per inserire eventuali altri moduli AngularJS richiesti dall&#39;app. Ad esempio, confrontate lo script precedente con l’implementazione di Geometrixx (disponibile all’indirizzo /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Per supportare la navigazione tra stati distinti nell&#39;app, lo script modulo-app-angolare esegue un&#39;iterazione in tutte le pagine discendenti della pagina dell&#39;app di livello principale per generare un set di &#39;route&#39; e configura ogni percorso nel servizio $routeProvider di Angular. Per un esempio di come si presenta nella pratica, osservate lo script del modulo angolare-app generato dall’esempio di app Geometrixx Outdoors: (il collegamento richiede un&#39;istanza locale) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Effettuando l&#39;accesso all&#39;AEMAngularApp generata, troverai una serie di route specificate come segue:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

L’esempio di cui sopra illustra in particolare un esempio di passaggio di un parametro come parte del percorso. In questo esempio stiamo indicando che quando un percorso che soddisfa il pattern specificato (/content/phonegap/geometrixx-outdoors/en/home/products/:id) è richiesto, deve essere gestito dal modello home/products.template e utilizzare il controller &#39;contentphonegapgeometrixxoutdoorsenhomeproducts&#39;.

Il modello da caricare quando questa route viene richiesta è specificato dalla proprietà templateUrl. Questo modello conterrà il codice HTML dei componenti AEM inclusi nella pagina, nonché eventuali direttive AngularJS necessarie per il cablaggio del lato client dell’applicazione. Per un esempio di direttiva AngularJS in un componente Geometrixx, osservate la riga 45 del template.jsp di swipe-carosello (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Controllori pagina {#page-controllers}

Nelle parole di Angular, &quot;un controller è una funzione di costruzione JavaScript utilizzata per ampliare l&#39;ambito angolare.&quot; ([sorgente](https://docs.angularjs.org/guide/controller)) Ogni pagina in un’app AEM viene automaticamente collegata a un controller che può essere incrementato da qualsiasi controller che specifica un `frameworkType` di `angular`. Osservate il componente ng-text come un esempio (/libs/mobileapps/components/angular/ng-text), incluso il nodo cq:template che verifica che ogni volta che questo componente viene aggiunto a una pagina includa questa importante proprietà.

Per un esempio di controller più complesso, aprite lo script ng-template-page controller.jsp (che si trova in /apps/geometrixx-outdoors-app/components/angular/ng-template-page). Di particolare interesse è il codice JavaScript generato al momento dell&#39;esecuzione, che viene riprodotto come segue:

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

Nell&#39;esempio precedente, noterete che stiamo prendendo un parametro dal `$routeParams` servizio e poi lo massaggiamo nella struttura di directory in cui sono memorizzati i nostri dati JSON. Trattando lo sku `id` in questo modo, siamo in grado di fornire un singolo modello di prodotto che può rappresentare i dati del prodotto per migliaia di prodotti potenzialmente distinti. Si tratta di un modello molto più scalabile che richiede un percorso singolo per ogni elemento in un database di prodotti (potenzialmente) di massa.

Sono inoltre disponibili due componenti: ng-product aumenta l’ambito con i dati estratti dalla `$http` chiamata precedente. In questa pagina è presente anche un&#39;immagine ng che a sua volta amplia l&#39;ambito con il valore recuperato dalla risposta. In virtù del `$http` servizio di Angular, ogni componente aspetterà pazientemente fino al completamento della richiesta e alla realizzazione della promessa che ha creato.

## Passaggi successivi {#the-next-steps}

Dopo aver appreso le applicazioni a pagina singola, consulta [Sviluppo di app con l’interfaccia CLI](/help/mobile/phonegap-apps-pg-cli.md)di PhoneGap.
