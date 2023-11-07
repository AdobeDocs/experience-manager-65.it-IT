---
title: Modelli di pagina per le app mobili
description: Segui questa pagina per ulteriori informazioni sui modelli di pagina. I componenti di pagina creati per la tua app si basano sul componente /libs/mobileapps/components/angular/ng-page.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 397def36-45b2-47a7-b103-99ca22b6dae1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2664'
ht-degree: 0%

---

# Modelli di pagina per le app mobili {#page-templates-for-mobile-apps}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

## Modelli di pagina per le app mobili {#page-templates-for-mobile-apps-1}

I componenti di pagina creati per la tua app si basano sul componente /libs/mobileapps/components/angular/ng-page ([apri in CRXDE Liti su un server locale](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Questo componente contiene i seguenti script JSP che il componente eredita o sostituisce:

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

Determina il nome dell&#39;applicazione utilizzando `applicationName` ed espone tramite la proprietà pageContext.

Include head.jsp e body.jsp.

### head.jsp {#head-jsp}

Scrive il `<head>` della pagina dell&#39;app.

Se desideri sovrascrivere la proprietà meta viewport dell’app, si tratta del file che sovrascrivi.

Seguendo le best practice, l’app include la porzione css delle librerie client nell’head, mentre JS è incluso nell’elemento &lt; `body>` elemento.

### body.jsp {#body-jsp}

Il rendering del corpo di una pagina di Angular viene eseguito in modo diverso a seconda che venga rilevato wcmMode (!= WCMMode.DISABLED) per determinare se la pagina viene aperta per la creazione o pubblicata.

**Modalità Autore**

In modalità di authoring, ogni singola pagina viene riprodotta separatamente. Angular non gestisce l’instradamento tra le pagine e non viene utilizzato un ng-view per caricare un modello parziale che contiene i componenti della pagina. Il contenuto del modello della pagina (template.jsp) viene invece incluso sul lato server tramite `cq:include` tag.

Questa strategia consente alle funzioni di authoring (come l’aggiunta e la modifica di componenti nel Sidekick paragrafo, nel sistema, nella modalità progettazione e così via) di funzionare senza modifiche. Le pagine che si basano sul rendering lato client, come quelle per le app, non funzionano bene in modalità di creazione AEM.

L’inclusione template.jsp è racchiusa in un `div` elemento che contiene `ng-controller` direttiva. Questa struttura consente il collegamento dei contenuti DOM al controller. Pertanto, anche se le pagine che si presentano sul lato client hanno esito negativo, i singoli componenti che lo fanno funzionano correttamente (vedi la sezione sui Componenti di seguito).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Modalità di pubblicazione**

In modalità di pubblicazione (ad esempio quando l’app viene esportata utilizzando Sincronizzazione contenuti), tutte le pagine diventano un’app a pagina singola (SPA). (Per informazioni sull’SPA, utilizza l’esercitazione Angular, in particolare [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Esiste una sola pagina HTML in un SPA (una pagina che contiene `<html>` elemento ). Questa pagina è nota come &quot;modello di layout&quot;. Nella terminologia di Angular, si tratta di &quot;...un modello comune a tutte le visualizzazioni presenti nella nostra applicazione&quot;. Considera questa pagina come la &quot;pagina dell’app di livello superiore&quot;. Per convenzione, la pagina dell’app di livello superiore è `cq:Page` nodo dell&#39;applicazione più vicino alla radice (che non è un reindirizzamento).

Poiché l’URI effettivo dell’app non cambia in modalità di pubblicazione, i riferimenti alle risorse esterne da questa pagina devono utilizzare percorsi relativi. Pertanto, viene fornito un componente immagine speciale che prende in considerazione questa pagina di livello principale durante il rendering delle immagini per l’esportazione.

In qualità di SPA, questa pagina di modello layout genera semplicemente un elemento div con una direttiva ng-view.

```xml
 <div ng-view ng-class="transition"></div>
```

Il servizio di routing di Angular utilizza questo elemento per visualizzare il contenuto di ogni pagina dell’app, incluso il contenuto modificabile della pagina corrente (contenuto in template.jsp).

Il file body.jsp include header.jsp e footer.jsp che sono vuoti. Se desideri fornire contenuto statico su ogni pagina, puoi ignorare questi script nell’app.

Infine, le clientlibs JavaScript sono incluse nella parte inferiore della sezione &lt;body> che include due file JS speciali generati sul server: *&lt;page name=&quot;&quot;>*.angular-app-module.js e *&lt;page name=&quot;&quot;>*.angular-app-controller.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Questo script definisce il modulo Angular dell’applicazione. L’output di questo script è collegato al markup generato dal resto del componente del modello tramite `html` in ng-page.jsp, che contiene il seguente attributo:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Questo attributo indica ad Angular che il contenuto di questo elemento DOM deve essere collegato al modulo seguente. Questo modulo collega le viste (in AEM sarebbero risorse cq:Page) ai controller corrispondenti.

Questo modulo definisce anche un controller di primo livello denominato `AppController` che espone `wcmMode` nell&#39;ambito e configura l&#39;URI dal quale recuperare i payload di aggiornamento di Sincronizzazione contenuto.

Infine, questo modulo scorre ogni pagina discendente (inclusa se stessa) ed esegue il rendering del contenuto del frammento di route di ogni pagina (tramite il selettore e l’estensione angular-route-fragment.js), includendolo come voce di configurazione in \$routeProvider di Angular. In altre parole, \$routeProvider indica all&#39;app il contenuto da riprodurre quando viene richiesto un determinato percorso.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Questo script genera un frammento JavaScript che deve avere la seguente forma:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Questo codice indica a $routeProvider (definito in angular-app-module.js.jsp) che &#39;/&lt;path>&#39; deve essere gestito dalla risorsa in `templateUrl`, e cablato da `controller` (che passeremo alla prossima).

Se necessario, puoi eseguire l’override di questo script per gestire percorsi più complessi, inclusi quelli con variabili. Un esempio è disponibile nello script /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp installato con AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

Ad Angular, i controller collegano le variabili nell&#39;ambito \$scope, esponendole alla visualizzazione. Lo script angular-app-controllers.js.jsp segue il pattern illustrato da angular-app-module.js.jsp, in quanto scorre ogni pagina discendente (inclusa se stessa) e restituisce il frammento del controller definito da ogni pagina (tramite controller.js.jsp). Il modulo che definisce viene chiamato `cqAppControllers` e devono essere elencati come una dipendenza del modulo app di livello superiore in modo che i controller di pagina siano disponibili.

### controller.js.jsp {#controller-js-jsp}

Lo script controller.js.jsp genera il frammento del controller per ogni pagina. Questo frammento di controller si presenta come segue:

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

Il `data` alla variabile viene assegnata la promessa restituita dall&#39;Angular `$http.get` metodo. Ogni componente incluso in questa pagina può, se necessario, rendere disponibile del contenuto .json (tramite il relativo script angular.json.jsp) e agire sul contenuto di questa richiesta quando viene risolta. La richiesta è molto veloce sui dispositivi mobili perché accede semplicemente al file system.

Affinché un componente possa far parte del controller in questo modo, è necessario estendere il componente /libs/mobileapps/components/angular/ng-component e includere `frameworkType: angular` proprietà.

### template.jsp {#template-jsp}

Introdotto per la prima volta nella sezione body.jsp, template.jsp contiene semplicemente il parsys della pagina. In modalità di pubblicazione, si fa riferimento direttamente a questo contenuto (in corrispondenza di &lt;page-path>.template.html) e caricato nell’SPA tramite templateUrl configurato in \$routeProvider.

I parsys in questo script possono essere configurati per accettare qualsiasi tipo di componente. Tuttavia, è necessario prestare attenzione quando si tratta di componenti creati per un sito web tradizionale (anziché per un SPA). Ad esempio, il componente immagine di base funziona correttamente solo sulla pagina dell’app di livello superiore, in quanto non è progettato per fare riferimento a risorse all’interno di un’app.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Questo script restituisce semplicemente le dipendenze di Angular del modulo app di Angular di livello superiore. Viene fatto riferimento da angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Uno script per posizionare il contenuto statico nella parte superiore dell’app. Questo contenuto viene incluso dalla pagina principale, al di fuori dell’ambito di ng-view.

### footer.jsp {#footer-jsp}

Uno script per inserire il contenuto statico nella parte inferiore dell’app. Questo contenuto viene incluso dalla pagina principale, al di fuori dell’ambito di ng-view.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Esegui l&#39;override di questo script per includere le clientlibs JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Sovrascrivi questo script per includere le clientlibs CSS.

## Componenti dell’app {#app-components}

I componenti dell’app non devono funzionare solo su un’istanza AEM (pubblicazione o authoring), ma anche quando il contenuto dell’applicazione viene esportato nel file system tramite Sincronizzazione contenuti. Il componente deve pertanto presentare le seguenti caratteristiche:

* È necessario fare riferimento in modo relativo a tutte le risorse, i modelli e gli script di un&#39;applicazione PhoneGap.
* La gestione dei collegamenti varia se l’istanza AEM funziona in modalità di authoring o pubblicazione.

### Risorse relative {#relative-assets}

L&#39;URI di una determinata risorsa in un&#39;applicazione PhoneGap differisce non solo per piattaforma, ma è univoco in ogni installazione dell&#39;app. Ad esempio, tieni presente il seguente URI di un’app in esecuzione nel simulatore iOS:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Si noti il GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; nel percorso.

In qualità di sviluppatore di PhoneGap, il contenuto che ti interessa si trova sotto la directory www. Per accedere alle risorse dell’app, usa i percorsi relativi.

Per aggravare il problema, l’applicazione PhoneGap utilizza il modello di app a pagina singola (SPA) in modo che l’URI di base (escluso l’hash) non cambi mai. Pertanto, ogni risorsa, modello o script a cui si fa riferimento **deve essere relativo alla pagina di livello principale.** La pagina di primo livello inizializza il routing e i controller Angular in virtù di `*<name>*.angular-app-module.js` e `*<name>*.angular-app-controllers.js`. Questa pagina deve essere quella più vicina alla directory principale dell’archivio che *non *estende un reindirizzamento sling:redirect.

Sono disponibili diversi metodi di supporto per gestire i percorsi relativi:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Per visualizzare alcuni esempi di utilizzo, apri l’origine mobileapps in /libs/mobileapps/components/angular.

### Collegamenti {#links}

I collegamenti devono utilizzare `ng-click="go('/path')"` per supportare tutte le modalità WCM. Questa funzione dipende dal valore di una variabile di ambito per determinare correttamente l’azione di collegamento:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Quando `$scope.wcmMode == true` gestiamo ogni evento di navigazione nel solito modo, in modo che il risultato sia una modifica al percorso e/o alla porzione di pagina dell’URL.

In alternativa, se `$scope.wcmMode == false`, ogni evento di navigazione determina una modifica alla porzione di hash dell’URL che viene risolta internamente dal modulo ngRoute di Angular.

### Dettagli script componente {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

Questo script visualizza il contenuto del componente o un segnaposto appropriato quando viene rilevata la modalità Modifica.

#### template.jsp {#template-jsp-1}

Lo script template.jsp esegue il rendering del markup del componente. Se il componente in questione è guidato da dati JSON estratti dall’AEM (ad esempio &quot;ng-text&quot;: /libs/mobileapps/components/angular/ng-text/template.jsp), questo script sarà responsabile del collegamento del markup con i dati esposti dall’ambito del controller della pagina.

Tuttavia, a volte i requisiti di prestazioni impongono di non eseguire la modellazione lato client (ovvero l’associazione dati). In questo caso, esegui semplicemente il rendering del markup del componente sul lato server e lo includi nel contenuto del modello della pagina.

#### overhead.jsp {#overhead-jsp}

Nei componenti guidati dai dati JSON (come &quot;ng-text&quot;: /libs/mobileapps/components/angular/ng-text), overhead.jsp può essere utilizzato per rimuovere tutto il codice Java da template.jsp. Viene quindi fatto riferimento da template.jsp e tutte le variabili da esso esposte nella richiesta sono disponibili per l’uso. Questa strategia incoraggia la separazione della logica dalla presentazione e limita la quantità di codice che deve essere copiata e incollata quando un nuovo componente viene derivato da uno esistente.

#### controller.js.jsp {#controller-js-jsp-1}

Come descritto in Modelli di pagina AEM, ogni componente può generare un frammento JavaScript per utilizzare il contenuto JSON esposto da `data` Promessa. Seguendo un Angular di convenzioni, un controller deve essere utilizzato solo per assegnare variabili all’ambito.

#### angular.json.jsp {#angular-json-jsp}

Questo script è incluso come frammento a livello di pagina &quot;&lt;page-name>File .angular.json&#39; che viene esportato per ogni pagina che estende ng-page. In questo file, lo sviluppatore del componente può esporre qualsiasi struttura JSON necessaria per il componente. Nell’esempio &quot;ng-text&quot;, questa struttura include semplicemente il contenuto di testo del componente e un flag che indica se il componente include o meno il testo RTF.

Il componente del prodotto app per Geometrixx in esterni è un esempio più complesso (/apps/geometrixx-outdoors-app/components/angular/ng-product):

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

## Contenuto del download di risorse CLI {#contents-of-the-cli-assets-download}

Scarica le risorse CLI dalla console delle app per ottimizzarle per una piattaforma specifica e quindi crea l’app utilizzando l’API CLI (Command Line Integration) di PhoneGap. Il contenuto del file ZIP salvato nel file system locale presenta la seguente struttura:

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

Si tratta di una directory nascosta che potrebbe non essere visualizzata a seconda delle impostazioni correnti del sistema operativo. Devi configurare il sistema operativo in modo che questa directory sia visibile se intendi modificare gli hook dell’app in essa contenuti.

#### .cordova/hook/ {#cordova-hooks}

Questa directory contiene [Hook CLI](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/). Le cartelle nella directory hook contengono script node.js eseguiti in punti esatti durante la generazione.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

La directory after-platform_add contiene `copy_AMS_Conifg.js` file. Questo script copia un file di configurazione per supportare la raccolta di dati analitici di Adobe Mobile Services.

#### .cordova/hook/after-preparation/ {#cordova-hooks-after-prepare}

La directory di post-preparazione contiene `copy_resource_files.js` file. Questo script copia diverse immagini di icone e schermate introduttive in posizioni specifiche della piattaforma.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

La directory before_platform_add contiene `install_plugins.js` file. Questo script scorre un elenco di identificatori del plug-in Cordova, installando quelli che rileva non sono già disponibili.

Questa strategia non richiede di raggruppare e installare i plug-in in AEM ogni volta che si utilizza Maven `content-package:install` viene eseguito. La strategia alternativa di archiviazione dei file nel sistema SCM richiede l&#39;installazione e il raggruppamento ripetitivi delle attività.

#### .cordova/hook/altri hook {#cordova-hooks-other-hooks}

Includi altri hook in base alle esigenze. Sono disponibili i seguenti hook (forniti dall&#39;app Phonegap sample hello world ):

* after_build
* before_build
* dopo_compilazione
* before_compile
* after_docs
* before_docs
* after_emulate
* prima_emulare
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
* dopo_preparare
* prima_preparare
* after_run
* before_run

#### piattaforme/ {#platforms}

Questa directory è vuota finché non esegui il comando `phonegap run <platform>` sul progetto. Attualmente, `<platform>` può essere `ios` o `android`.

Dopo aver generato l’app per una piattaforma specifica, viene creata la directory corrispondente che contiene il codice dell’app specifico per la piattaforma.

#### plug-in/ {#plugins}

La directory dei plug-in viene compilata da ogni plug-in elencato in `.cordova/hooks/before_platform_add/install_plugins.js` dopo l&#39;esecuzione di `phonegap run <platform>` comando. La directory è inizialmente vuota.

#### www/ {#www}

La directory www contiene tutti i contenuti web (file HTML, JS e CSS) che implementano l’aspetto e il comportamento dell’app. Ad eccezione delle eccezioni descritte di seguito, questo contenuto proviene dall’AEM e viene esportato nel suo formato statico tramite Content Sync.

#### www/config.xml {#www-config-xml}

Documentazione di PhoneGap (`https://docs.phonegap.com`) fa riferimento a questo file come a un &quot;file di configurazione globale&quot;. Il file config.xml contiene molte proprietà dell’app, come il nome dell’app, le preferenze dell’app (ad esempio, se una visualizzazione web di iOS consente o meno l’overscroll) e le dipendenze dei plug-in che sono *solo* utilizzato da PhoneGap Build.

Il file config.xml è un file statico in AEM ed è esportato così com’è tramite Content Sync.

#### www/index.html {#www-index-html}

Il file index.html viene reindirizzato alla pagina iniziale dell’app.

Il file config.xml contiene `content` elemento:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

Nella documentazione di PhoneGap (`https://docs.phonegap.com`), questo elemento è descritto come &quot;L&#39;elemento facoltativo &lt;content> definisce la pagina iniziale dell’app nella directory delle risorse web di livello superiore. Il valore predefinito è index.html, che in genere viene visualizzato nella directory www di primo livello di un progetto.&quot;

PhoneGap Build non riesce se non è presente un file index.html. Pertanto, questo file è incluso.

#### www/res {#www-res}

La directory res contiene immagini e icone della schermata iniziale. Il `copy_resource_files.js` copia i file nelle posizioni specifiche della piattaforma durante il `after_prepare` fase di build.

#### www/etc {#www-etc}

Per convenzione, nell’AEM il nodo /etc contiene contenuto statico clientlib. La directory etc contiene le librerie Topcoat, AngularJS e Geometrixx-clientlibsall.

#### www/apps {#www-apps}

La directory delle app contiene il codice relativo alla pagina iniziale. La caratteristica unica della pagina iniziale di un’app AEM è che inizializza l’app senza alcuna interazione da parte dell’utente. Il contenuto clientlib (sia CSS che JS) dell’app è quindi minimo per massimizzare le prestazioni.

#### www/content {#www-content}

La directory dei contenuti contiene il resto del contenuto web dell’app. Il contenuto può includere, ma non è limitato a, i seguenti file:

* Contenuto della pagina HTML, creata direttamente nell’AEM
* Risorse di immagini associate ai componenti AEM
* Contenuto JavaScript generato dagli script lato server
* File JSON che descrivono il contenuto della pagina o del componente

#### www/package.json {#www-package-json}

Il file package.json è un file manifesto che elenca i file che **completo** Il download di Sincronizzazione contenuti include. Questo file contiene anche la marca temporale in corrispondenza della quale è stato generato il payload di sincronizzazione dei contenuti (`lastModified`). Questa proprietà viene utilizzata quando si richiedono aggiornamenti parziali dell’app dall’AEM.

#### www/package-update.json {#www-package-update-json}

Se il payload è un download dell’intera app, il manifesto contiene l’elenco esatto dei file come `package.json`.

Tuttavia, se questo payload è un aggiornamento parziale, `package-update.json` contiene solo i file inclusi in questo particolare payload.
