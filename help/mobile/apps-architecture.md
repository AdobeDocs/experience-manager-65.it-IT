---
title: Modelli di pagina per app mobili
seo-title: Modelli di pagina per app mobili
description: Seguite questa pagina per ulteriori informazioni sui modelli di pagina. I componenti pagina creati per l’app si basano sul componente /libs/mobileapps/components/angular/ng-page.
seo-description: Seguite questa pagina per ulteriori informazioni sui modelli di pagina. I componenti pagina creati per l’app si basano sul componente /libs/mobileapps/components/angular/ng-page.
uuid: c53901c9-5974-4c6b-ac61-1c094a93c9d6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: cfc7ad16-965e-4075-bc4d-5630abeaba55
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2698'
ht-degree: 0%

---


# Modelli di pagina per app mobili {#page-templates-for-mobile-apps}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

## Modelli di pagina per app mobili {#page-templates-for-mobile-apps-1}

I componenti di pagina creati per l&#39;app si basano sul componente /libs/mobileapps/components/angular/ng-page ([aperto in CRXDE Lite su un server locale](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Questo componente contiene i seguenti script JSP che il componente eredita o sostituisce:

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

Determina il nome dell&#39;applicazione utilizzando la proprietà `applicationName` ed espone l&#39;applicazione tramite pageContext.

Include head.jsp e body.jsp.

### head.jsp {#head-jsp}

Inserisce l&#39;elemento `<head>` della pagina dell&#39;app.

Se desiderate sovrascrivere la proprietà meta viewport dell&#39;app, questo è il file che avete ignorato.

Come best practice, l&#39;app include la parte css delle librerie client nella sezione head, mentre JS è incluso nell&#39;elemento &lt; `body>` di chiusura.

### body.jsp {#body-jsp}

Il corpo di una pagina Angular viene rappresentato in modo diverso a seconda che wcmMode venga rilevato (!= WCMMode.DISABLED) per determinare se la pagina viene aperta per la creazione o come pagina pubblicata.

**Modalità autore**

In modalità di creazione, ogni singola pagina viene rappresentata separatamente. Angular non gestisce il routing tra le pagine, né un ng-view utilizzato per caricare un modello parziale che contiene i componenti della pagina. Al contrario, il contenuto del modello di pagina (template.jsp) viene incluso sul lato server tramite il tag `cq:include`.

Questa strategia consente alle funzioni di authoring (come l’aggiunta e la modifica di componenti nel sistema paragrafo, nella barra laterale, in modalità progettazione ecc.) per funzionare senza modifiche. Le pagine che si basano sul rendering lato client, come quelle per le app, non funzionano bene in AEM modalità di creazione.

Tenere presente che template.jsp include è racchiuso in un elemento `div` che contiene la direttiva `ng-controller`. Questa struttura consente il collegamento dei contenuti DOM con il controller. Pertanto, anche se le pagine che si presentano sul lato client non vanno a buon fine, i singoli componenti che lo fanno funzionano correttamente (vedere la sezione sui componenti di seguito).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Modalità di pubblicazione**

In modalità di pubblicazione (ad esempio, quando l&#39;app viene esportata tramite Content Sync), tutte le pagine diventano un&#39;app a pagina singola (SPA). Per informazioni su SPA, utilizzate l&#39;esercitazione angolare, in particolare [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).

In un SPA è presente una sola pagina HTML (una pagina che contiene l&#39;elemento `<html>`). Questa pagina è nota come &quot;modello di layout&quot;. In terminologia angolare, è &quot;...un modello comune per tutte le viste della nostra applicazione.&quot; Considerate questa pagina come &quot;pagina dell&#39;app di livello principale&quot;. Per convenzione, la pagina dell&#39;app di livello principale è il nodo `cq:Page` dell&#39;applicazione più vicino alla radice (e non è un reindirizzamento).

Poiché l’URI effettivo dell’app non cambia in modalità di pubblicazione, i riferimenti a risorse esterne da questa pagina devono utilizzare percorsi relativi. Di conseguenza, quando si esegue il rendering delle immagini per l’esportazione viene fornito un componente immagine speciale che tiene conto di questa pagina di livello principale.

Come SPA, questa pagina modello di layout genera semplicemente un elemento div con una direttiva ng-view.

```xml
 <div ng-view ng-class="transition"></div>
```

Il servizio di route angolare utilizza questo elemento per visualizzare il contenuto di ogni pagina dell&#39;app, incluso il contenuto autorizzabile della pagina corrente (contenuto in template.jsp).

Il file body.jsp include header.jsp e footer.jsp vuoti. Se desiderate fornire contenuto statico su ogni pagina, potete ignorare questi script nell&#39;app.

Infine, i clientlibs javascript sono inclusi nella parte inferiore dell&#39;elemento &lt;body>, inclusi due file JS speciali generati sul server: *&lt;nome pagina>*.angular-app-module.js e *&lt;nome pagina>*.angular-app-controller.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Questo script definisce il modulo Angular dell&#39;applicazione. L&#39;output di questo script è collegato alla marcatura generata dal resto del componente del modello tramite l&#39;elemento `html` in ng-page.jsp, che contiene il seguente attributo:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Questo attributo indica ad Angular che il contenuto di questo elemento DOM deve essere collegato al seguente modulo. Questo modulo collega le viste (in AEM queste sarebbero risorse cq:Page) con i controller corrispondenti.

Questo modulo definisce anche un controller di livello principale denominato `AppController` che espone la variabile `wcmMode` all&#39;ambito e configura l&#39;URI dal quale recuperare i payload di aggiornamento della sincronizzazione dei contenuti.

Infine, questo modulo esegue un&#39;iterazione su ciascuna pagina discendente (inclusa se stessa) ed esegue il rendering del contenuto della frazione di route di ciascuna pagina (tramite il selettore e l&#39;estensione angular-route-fragment.js), incluso come voce di configurazione in \$routeProvider di Angular. In altre parole, \$routeProvider indica all&#39;app quale contenuto eseguire il rendering quando viene richiesto un determinato percorso.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Questo script genera un frammento JavaScript che deve avere il seguente modulo:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Questo codice indica a $routeProvider (definito in angular-app-module.js.jsp) che &#39;/&lt;percorso>&#39; deve essere gestito dalla risorsa in `templateUrl`, e cablato da `controller` (che verrà raggiunto dopo).

Se necessario, è possibile ignorare questo script per gestire percorsi più complessi, inclusi quelli con variabili. Un esempio è riportato nello script /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp installato con AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

In Angular, i controller collegano le variabili nell&#39;ambito \$scope, esponendole alla vista. Lo script angular-app-controllers.js.jsp segue il pattern illustrato da angular-app-module.js.jsp, in quanto esegue un&#39;iterazione su ciascuna pagina discendente (inclusa se stessa) e genera il frammento di controller definito da ogni pagina (tramite controller.js.jsp). Il modulo che definisce è denominato `cqAppControllers` e deve essere elencato come una dipendenza del modulo app di livello principale in modo da rendere disponibili i controller di pagina.

### controller.js.jsp {#controller-js-jsp}

Lo script controller.js.jsp genera il frammento controller per ogni pagina. Questo frammento controller ha il seguente modulo:

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

Alla variabile `data` viene assegnata la promessa restituita dal metodo Angular `$http.get`. Ogni componente incluso in questa pagina può, se lo desiderate, rendere disponibile del contenuto .json (tramite il relativo script angular.json.jsp) e agire sul contenuto di questa richiesta quando viene risolta. La richiesta è molto veloce su dispositivi mobili perché accede semplicemente al file system.

Affinché un componente faccia parte del controller in questo modo, deve estendere il componente /libs/mobileapps/components/angular/ng-component e includere la proprietà `frameworkType: angular`.

### template.jsp {#template-jsp}

Introdotto nella sezione body.jsp, template.jsp contiene semplicemente parsys della pagina. In modalità di pubblicazione, a questo contenuto viene fatto riferimento direttamente (in &lt;percorso-pagina>.template.html) e caricato nel SPA tramite templateUrl configurato su \$routeProvider.

parsys in questo script può essere configurato per accettare qualsiasi tipo di componente. Tuttavia, occorre prestare attenzione quando si tratta di componenti creati per un sito Web tradizionale (anziché per un SPA). Ad esempio, il componente Immagine di base funziona correttamente solo sulla pagina dell&#39;app di livello principale, in quanto non è progettato per fare riferimento a risorse che si trovano all&#39;interno di un&#39;app.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Questo script genera semplicemente le dipendenze Angular del modulo app Angular di livello superiore. Vi viene fatto riferimento da angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Uno script per posizionare il contenuto statico nella parte superiore dell&#39;app. Questo contenuto è incluso nella pagina di livello principale, al di fuori dell’ambito della visualizzazione ng.

### footer.jsp {#footer-jsp}

Uno script per inserire contenuto statico nella parte inferiore dell&#39;app. Questo contenuto è incluso nella pagina di livello principale, al di fuori dell’ambito della visualizzazione ng.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Ignorate questo script per includere i clientlibs JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Ignorate questo script per includere i clientlibs CSS.

## Componenti app {#app-components}

I componenti dell&#39;app non devono funzionare solo su un&#39;istanza AEM (pubblicazione o creazione), ma anche quando il contenuto dell&#39;applicazione viene esportato nel file system tramite Content Sync. Il componente deve pertanto includere le seguenti caratteristiche:

* È necessario fare riferimento a tutte le risorse, i modelli e gli script di un&#39;applicazione PhoneGap relativamente.
* La gestione dei collegamenti è diversa se l’istanza AEM funziona in modalità di creazione o pubblicazione.

### Risorse relative {#relative-assets}

L&#39;URI di una risorsa specifica in un&#39;applicazione PhoneGap non differisce solo per piattaforma, ma è univoco per ogni installazione dell&#39;app. Ad esempio, prendete nota del seguente URI di un&#39;app in esecuzione in iOS Simulator:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Osservare il GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; nel percorso.

Come sviluppatore di PhoneGap, il contenuto a cui siete interessati si trova sotto la directory www. Per accedere alle risorse dell&#39;app, usa percorsi relativi.

Per risolvere il problema, l&#39;applicazione PhoneGap utilizza il pattern app (SPA) a pagina singola in modo che l&#39;URI di base (escluso l&#39;hash) non cambi mai. Di conseguenza, ogni risorsa, modello o script a cui si fa riferimento **deve essere relativo alla pagina di livello principale.** La pagina di primo livello inizializza il routing Angular e i controller in virtù  `*<name>*.angular-app-module.js` e  `*<name>*.angular-app-controllers.js`. Questa pagina deve essere la pagina più vicina alla radice del repository che *non si estende una sling:redirect.

Sono disponibili diversi metodi helper per per gestire i percorsi relativi:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Per visualizzare esempi del loro utilizzo, aprite l&#39;origine mobileapps disponibile in /libs/mobileapps/components/angular.

### Collegamenti {#links}

I collegamenti devono utilizzare la funzione `ng-click="go('/path')"` per supportare tutte le modalità WCM. Questa funzione dipende dal valore di una variabile di ambito per determinare correttamente l&#39;azione del collegamento:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Quando `$scope.wcmMode == true` gestiamo ogni evento di navigazione nel modo usuale, in modo che il risultato sia una modifica al percorso e/o alla parte di pagina dell&#39;URL.

In alternativa, se `$scope.wcmMode == false`, ogni evento di navigazione produce una modifica alla porzione hash dell&#39;URL, risolta internamente dal modulo ngRoute di Angular.

### Dettagli script componente {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

Questo script visualizza il contenuto del componente o un segnaposto appropriato quando viene rilevata la modalità di modifica.

#### template.jsp {#template-jsp-1}

Lo script template.jsp esegue il rendering della marcatura del componente. Se il componente in questione è guidato da dati JSON estratti da AEM (come &quot;ng-text&quot;): /libs/mobileapps/components/angular/ng-text/template.jsp), questo script sarà responsabile del cablaggio della marcatura con i dati esposti dall&#39;ambito del controller della pagina.

Tuttavia, a volte i requisiti di prestazioni stabiliscono che non è possibile eseguire modelli lato client (ovvero il binding dei dati). In questo caso, è sufficiente eseguire il rendering della marcatura del componente sul lato server e viene inclusa nel contenuto del modello di pagina.

#### overhead.jsp {#overhead-jsp}

Nei componenti guidati da dati JSON (come &#39;ng-text&#39;: /libs/mobileapps/components/angular/ng-text), overhead.jsp può essere utilizzato per rimuovere tutto il codice Java da template.jsp. Viene quindi fatto riferimento a template.jsp e tutte le variabili che espone sulla richiesta sono disponibili per l&#39;uso. Questa strategia incoraggia la separazione della logica dalla presentazione e limita la quantità di codice da copiare e incollare quando un nuovo componente viene derivato da uno esistente.

#### controller.js.jsp {#controller-js-jsp-1}

Come descritto in AEM modelli di pagina, ogni componente può restituire un frammento JavaScript per utilizzare il contenuto JSON esposto dalla promessa `data`. In base alle convenzioni Angular, è consigliabile utilizzare un controller solo per assegnare variabili all&#39;ambito.

#### angular.json.jsp {#angular-json-jsp}

Questo script è incluso come frammento nel file &#39;&lt;page-name>.angular.json&#39; a livello di pagina, che viene esportato per ogni pagina che si estende su più pagine. In questo file, lo sviluppatore di componenti può esporre qualsiasi struttura JSON richiesta dal componente. Nell’esempio &quot;ng-text&quot;, questa struttura include semplicemente il contenuto di testo del componente e un flag che indica se il componente include o meno testo RTF.

Il componente di prodotto per app in esterni è un esempio più complesso (/apps/geometrixx-outdoors-app/components/angular/ng-product):

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## Contenuto del download delle risorse CLI {#contents-of-the-cli-assets-download}

Scaricate le risorse CLI dalla console App per ottimizzarle per una piattaforma specifica e quindi create l&#39;app utilizzando l&#39;API CLI (Command Line Integration) di PhoneGap. Il contenuto del file ZIP salvato nel file system locale ha la struttura seguente:

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

Si tratta di una directory nascosta che potrebbe non essere visibile a seconda delle impostazioni del sistema operativo in uso. È necessario configurare il sistema operativo in modo che questa directory sia visibile se si prevede di modificare gli hook dell&#39;app che contiene.

#### .cordova/ganci/ {#cordova-hooks}

Questa directory contiene i ganci [CLI](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/). Le cartelle nella directory degli hook contengono script node.js che vengono eseguiti nei punti esatti durante la creazione.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

La directory after-platform_add contiene il file `copy_AMS_Conifg.js`. Questo script copia un file di configurazione per supportare la raccolta  analisi di Mobile Services.

#### .cordova/ganci/post-preparazione/ {#cordova-hooks-after-prepare}

La directory post-preparazione contiene il file `copy_resource_files.js`. Questo script copia una serie di immagini di icone e schermate iniziali in posizioni specifiche per la piattaforma.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

La directory before_platform_add contiene il file `install_plugins.js`. Questo script esegue un&#39;iterazione in un elenco di identificatori plug-in Cordova, installando quelli che rileva non sono già disponibili.

Questa strategia non richiede la creazione di pacchetti e l&#39;installazione dei plug-in per AEM ogni volta che viene eseguito il comando Maven `content-package:install`. La strategia alternativa per il controllo dei file nel sistema SCM richiede attività di bundling e installazione ripetitive.

#### .cordova/ganci/altri ganci {#cordova-hooks-other-hooks}

Includere altri ganci come necessario. Sono disponibili i seguenti ganci (forniti dall&#39;app di esempio Phonegap hello world):

* after_build
* before_build
* after_compila
* before_compilare
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_Prepare
* before_Prepare
* after_run
* before_run

#### platform/ {#platforms}

Questa directory è vuota finché non si esegue il comando `phonegap run <platform>` nel progetto. Attualmente, `<platform>` può essere `ios` o `android`.

Dopo aver creato l&#39;app per una piattaforma specifica, viene creata la directory corrispondente e contiene il codice dell&#39;app specifico per la piattaforma.

#### plugins/ {#plugins}

La directory dei plug-in viene compilata da ciascun plug-in elencato nel file `.cordova/hooks/before_platform_add/install_plugins.js` dopo l&#39;esecuzione del comando `phonegap run <platform>`. La directory inizialmente è vuota.

#### www/ {#www}

La directory www contiene tutto il contenuto Web (file HTML, JS e CSS) che implementa l&#39;aspetto e il comportamento dell&#39;app. Ad eccezione delle eccezioni descritte di seguito, il contenuto proviene da AEM ed è esportato nel suo modulo statico tramite Content Sync.

#### www/config.xml {#www-config-xml}

La [documentazione di PhoneGap](https://docs.phonegap.com) fa riferimento a questo file come &quot;file di configurazione globale&quot;. Il file config.xml contiene molte proprietà dell&#39;app, come il nome dell&#39;app, le &#39;preferenze&#39; dell&#39;app (ad esempio, se una visualizzazione Web iOS consente o meno lo scorrimento eccessivo) e le dipendenze del plug-in che sono *solo* utilizzate dalla build PhoneGap.

Il file config.xml è un file statico in AEM ed è esportato così come lo è tramite Content Sync.

#### www/index.html {#www-index-html}

Il file index.html viene reindirizzato alla pagina iniziale dell&#39;app.

Il file config.xml contiene l&#39;elemento `content`:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

In [la documentazione di PhoneGap](https://docs.phonegap.com), questo elemento è descritto come &quot;L&#39;elemento &lt;content> facoltativo definisce la pagina iniziale dell&#39;app nella directory delle risorse Web di livello principale. Il valore predefinito è index.html, che di solito viene visualizzato nella directory www di livello principale di un progetto.&quot;

PhoneGap build non riesce se non è presente un file index.html. Pertanto, questo file è incluso.

#### www/res {#www-res}

La directory res contiene immagini della schermata iniziale e icone. Lo script `copy_resource_files.js` copia i file nei percorsi specifici della piattaforma durante la fase di creazione `after_prepare`.

#### www/etc {#www-etc}

Per convenzione, in AEM nodo /etc contiene contenuto clientlib statico. La directory etc contiene le librerie Topcappotto, AngularJS e Geometrixx-clientlibsall.

#### www/apps {#www-apps}

La directory delle app contiene il codice relativo alla pagina iniziale. La caratteristica unica della pagina iniziale di un&#39;app AEM è che essa inizializza l&#39;app senza alcuna interazione con l&#39;utente. Il contenuto clientlib (sia CSS che JS) dell&#39;app è quindi minimo per massimizzare le prestazioni.

#### www/content {#www-content}

La directory del contenuto contiene il resto del contenuto Web dell&#39;app. Il contenuto può includere, ma non solo, i file seguenti:

* Contenuto della pagina HTML, creato direttamente in AEM
* Risorse di immagine associate ai componenti AEM
* Contenuto JavaScript generato dagli script sul lato server
* File JSON che descrivono il contenuto di una pagina o di un componente

#### www/package.json {#www-package-json}

Il file package.json è un file manifesto che elenca i file inclusi nel download di **full** Content Sync. Questo file contiene anche la marca temporale in cui è stato generato il payload di sincronizzazione dei contenuti (`lastModified`). Questa proprietà viene utilizzata per richiedere aggiornamenti parziali dell&#39;app da AEM.

#### www/package-update.json {#www-package-update-json}

Se questo payload è un download dell&#39;intera app, il manifesto contiene l&#39;elenco esatto dei file come `package.json`.

Tuttavia, se questo payload è un aggiornamento parziale, `package-update.json` contiene solo i file inclusi in questo particolare payload.
