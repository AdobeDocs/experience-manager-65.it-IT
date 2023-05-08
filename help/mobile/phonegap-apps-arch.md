---
title: L'anatomia di un'app
seo-title: The Anatomy of an App
description: Questa pagina fornisce una descrizione dei componenti della pagina creati per la tua app in base al componente /libs/mobileapps/components/angular/ng-page (CRXDE Lite su un server locale).
seo-description: This page provides description of the page components that you create for your app are based on the /libs/mobileapps/components/angular/ng-page component (CRXDE Lite on a local server).
uuid: 4c1a74c1-85af-4a79-b723-e9fbfc661d35
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 55667e62-a61b-4794-b292-8d54929c41ac
exl-id: ab4f1c61-be83-420e-a339-02cf1f33efed
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '2691'
ht-degree: 0%

---

# L&#39;anatomia di un&#39;app{#the-anatomy-of-an-app}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

## Modelli di pagina per le app mobili {#page-templates-for-mobile-apps}

I componenti pagina creati per la tua app si basano sul componente /libs/mobileapps/components/angular/ng-page ([aprire in CRXDE Lite su un server locale](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Questo componente contiene i seguenti script JSP che il componente eredita o sostituisce:

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

Determina il nome dell&#39;applicazione utilizzando `applicationName` e lo espone tramite pageContext.

Include head.jsp e body.jsp.

### head.jsp {#head-jsp}

Scrive il `<head>` della pagina dell’app.

Se desideri ignorare la proprietà meta viewport dell&#39;app, si tratta del file che sovrascrivi.

Di seguito sono riportate le best practice, l’app include la parte css delle librerie client nella sezione head, mentre JS è incluso nella &lt; di chiusura `body>` elemento.

### body.jsp {#body-jsp}

Il corpo di una pagina di Angular viene rappresentato in modo diverso a seconda che wcmMode venga rilevato (!= WCMMode.DISABLED) per determinare se la pagina viene aperta per l’authoring o come pagina pubblicata.

**Modalità Autore**

In modalità di authoring, ogni singola pagina viene riprodotta separatamente. Angular non gestisce il routing tra le pagine, né un ng-view utilizzato per caricare un modello parziale che contiene i componenti della pagina. Invece, il contenuto del modello di pagina (template.jsp) è incluso sul lato server tramite il `cq:include` tag .

Questa strategia abilita le funzioni di authoring (ad esempio l’aggiunta e la modifica di componenti nel sistema di paragrafi, nella barra laterale, in modalità progettazione, ecc.) per funzionare senza modifiche. Le pagine che si basano sul rendering lato client, come quelle per le app, non funzionano bene in modalità di authoring AEM.

Tieni presente che template.jsp include è racchiuso in un `div` che contiene `ng-controller` direttiva. Questa struttura consente il collegamento del contenuto DOM con il controller. Pertanto, anche se le pagine con rendering sul lato client non riescono, i singoli componenti che lo fanno funzionano correttamente (consulta la sezione sui componenti di seguito).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Modalità di pubblicazione**

In modalità di pubblicazione (ad esempio quando l’app viene esportata tramite Content Sync), tutte le pagine diventano un’app a pagina singola (SPA). (Per informazioni su SPA, utilizza l’esercitazione di Angular, in particolare [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

C&#39;è una sola pagina HTML in un SPA (una pagina che contiene il `<html>` elemento). Questa pagina è nota come &quot;modello di layout&quot;. Nella terminologia Angular, è &quot;...un modello comune per tutte le visualizzazioni nella nostra applicazione.&quot; Considera questa pagina come la &quot;pagina dell’app di livello principale&quot;. Per convenzione, la pagina dell’app di livello principale è la `cq:Page` nodo dell&#39;applicazione più vicino alla radice (e non è un reindirizzamento).

Poiché l’URI effettivo dell’app non cambia in modalità di pubblicazione, i riferimenti a risorse esterne da questa pagina devono utilizzare percorsi relativi. Pertanto, viene fornito un componente immagine speciale che prende in considerazione questa pagina di primo livello durante il rendering delle immagini per l’esportazione.

Come SPA, questa pagina del modello di layout genera semplicemente un elemento div con una direttiva ng-view.

```xml
 <div ng-view ng-class="transition"></div>
```

Il servizio di route di Angular utilizza questo elemento per visualizzare il contenuto di ogni pagina dell&#39;app, incluso il contenuto autorizzabile della pagina corrente (contenuto in template.jsp).

Il file body.jsp include header.jsp e footer.jsp vuoti. Se desideri fornire contenuto statico su ogni pagina, puoi sovrascrivere questi script nell’app.

Infine, le clientlib javascript sono incluse nella parte inferiore della &lt;body> elemento che include due file JS speciali generati sul server: *&lt;page name=&quot;&quot;>*.angular-app-module.js e *&lt;page name=&quot;&quot;>*.angular-app-controller.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Questo script definisce il modulo di Angular dell&#39;applicazione. L’output di questo script è collegato al markup generato dal resto del componente del modello tramite il `html` in ng-page.jsp, che contiene il seguente attributo:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Questo attributo indica ad Angular che il contenuto di questo elemento DOM deve essere collegato al seguente modulo. Questo modulo collega le visualizzazioni (in AEM queste sarebbero risorse cq:Page) con i controller corrispondenti.

Questo modulo definisce anche un controller di livello superiore denominato `AppController` che espone `wcmMode` nell’ambito e configura l’URI da cui recuperare i payload dell’aggiornamento di Content Sync.

Infine, questo modulo esegue l’iterazione su ogni pagina discendente (incluso se stesso) ed esegue il rendering del contenuto della gestione del percorso di ogni pagina (tramite il selettore e l’estensione angular-route-fragment.js), incluso come voce di configurazione in $routeProvider di Angular. In altre parole, $routeProvider indica all&#39;app quale contenuto eseguire il rendering quando viene richiesto un determinato percorso.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Questo script genera un frammento JavaScript che deve avere il seguente modulo:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Questo codice indica a $routeProvider (definito in angular-app-module.js.jsp) che &#39;/&lt;path>&quot; deve essere gestito dalla risorsa in `templateUrl`e collegati da `controller` (che passeremo al prossimo).

Se necessario, puoi sovrascrivere questo script per gestire percorsi più complessi, inclusi quelli con variabili. Un esempio di questo è visibile nello script /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp installato con AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

Ad Angular, i titolari del trattamento collegano le variabili nell&#39;ambito $scope, esponendole alla visualizzazione. Lo script angular-app-controllers.js.jsp segue il pattern illustrato da angular-app-module.js.jsp in quanto esegue iterazioni attraverso ogni pagina discendente (incluso se stesso) e produce il frammento di controller definito da ogni pagina (tramite controller.js.jsp). Il modulo che definisce è denominato `cqAppControllers` e deve essere elencato come una dipendenza del modulo app di livello superiore in modo che i controller di pagina siano resi disponibili.

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

Tieni presente che `data` viene assegnata la promessa restituita dall’Angular `$http.get` metodo . Ogni componente incluso in questa pagina può, se lo desideri, rendere disponibile alcuni contenuti .json (tramite il suo script angular.json.jsp) e agire sul contenuto di questa richiesta quando viene risolto. La richiesta è molto veloce su dispositivi mobili perché accede semplicemente al file system.

Affinché un componente faccia parte del controller in questo modo, deve estendere il componente /libs/mobileapps/components/angular/ng-component e includere il `frameworkType: angular` proprietà.

### template.jsp {#template-jsp}

Introdotto per la prima volta nella sezione body.jsp, template.jsp contiene semplicemente il parsys della pagina. In modalità di pubblicazione, a questo contenuto viene fatto riferimento direttamente (in &lt;page-path>.template.html) e caricato nel SPA tramite il templateUrl configurato sul $routeProvider.

Il parsys in questo script può essere configurato per accettare qualsiasi tipo di componente. Tuttavia, occorre prestare attenzione quando si tratta di componenti creati per un sito web tradizionale (anziché per un SPA). Ad esempio, il componente Immagine di base funziona correttamente solo sulla pagina dell’app di livello principale, in quanto non è progettato per fare riferimento a risorse che si trovano all’interno di un’app.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Questo script genera semplicemente le dipendenze Angular del modulo app di Angular di livello superiore. È referenziato da angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Uno script per inserire contenuto statico nella parte superiore dell’app. Questo contenuto è incluso nella pagina di primo livello, al di fuori dell’ambito della visualizzazione ng.

### footer.jsp {#footer-jsp}

Uno script per inserire contenuto statico nella parte inferiore dell’app. Questo contenuto è incluso nella pagina di primo livello, al di fuori dell’ambito della visualizzazione ng.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Ignora questo script per includere le clientlibs JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Ignora questo script per includere le clientlib CSS.

## Componenti app {#app-components}

I componenti dell’app non devono funzionare solo su un’istanza AEM (pubblicazione o authoring), ma anche quando il contenuto dell’applicazione viene esportato nel file system tramite Content Sync. Il componente deve pertanto comprendere le seguenti caratteristiche:

* È necessario fare riferimento a tutte le risorse, ai modelli e agli script di un’applicazione PhoneGap in modo relativamente semplice.
* La gestione dei collegamenti differisce se l’istanza AEM funziona in modalità di authoring o pubblicazione.

### Risorse relative {#relative-assets}

L’URI di una determinata risorsa in un’applicazione PhoneGap differisce non solo per piattaforma, ma è univoco in ogni installazione dell’app. Ad esempio, prendi nota del seguente URI di un’app in esecuzione nel simulatore iOS:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Si noti il GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; nel percorso.

In qualità di sviluppatore PhoneGap, il contenuto di cui sei interessato si trova sotto la directory www. Per accedere alle risorse dell’app, usa percorsi relativi.

Per risolvere il problema, l’applicazione PhoneGap utilizza il pattern di app a pagina singola (SPA) in modo che l’URI di base (escluso l’hash) non cambi mai. Pertanto, ogni risorsa, modello o script a cui fai riferimento **deve essere relativo alla pagina di livello principale. **La pagina di livello superiore inizializza il routing e i controller di Angular in virtù di `*<name>*.angular-app-module.js` e `*<name>*.angular-app-controllers.js`. Questa pagina deve essere la pagina più vicina alla radice del repository che *non *estende un sling:redirect.

Sono disponibili diversi metodi helper per per gestire i percorsi relativi:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Per visualizzare esempi di utilizzo, apri l’origine mobileapps disponibile in /libs/mobileapps/components/angular.

### Collegamenti {#links}

I collegamenti devono utilizzare `ng-click="go('/path')"` per supportare tutte le modalità WCM. Questa funzione dipende dal valore di una variabile di ambito per determinare correttamente l&#39;azione di collegamento:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Quando `$scope.wcmMode == true` gestiamo ogni evento di navigazione nel modo consueto, in modo che il risultato sia una modifica al percorso e/o alla parte di pagina dell’URL.

In alternativa, se `$scope.wcmMode == false`, ogni evento di navigazione comporta una modifica della parte hash dell’URL che viene risolta internamente dal modulo ngRoute di Angular.

### Dettagli script componente {#component-script-details}

![chlimage_1-144](assets/chlimage_1-144.png)

#### ng-component.jsp {#ng-component-jsp}

Questo script visualizza il contenuto del componente o un segnaposto appropriato quando viene rilevata la modalità Modifica .

#### template.jsp {#template-jsp-1}

Lo script template.jsp esegue il rendering del markup del componente. Se il componente in questione è guidato da dati JSON estratti da AEM (come &quot;ng-text&quot;): /libs/mobileapps/components/angular/ng-text/template.jsp), quindi questo script sarà responsabile del cablaggio del markup con i dati esposti dall&#39;ambito di controllo della pagina.

Tuttavia, a volte i requisiti di prestazioni determinano l’assenza di modelli lato client (alias binding dei dati). In questo caso, è sufficiente eseguire il rendering del markup del componente sul lato server ed è incluso nel contenuto del modello di pagina.

#### overhead.jsp {#overhead-jsp}

Nei componenti gestiti da dati JSON (come &quot;ng-text&quot;): /libs/mobileapps/components/angular/ng-text), overhead.jsp può essere utilizzato per rimuovere tutto il codice Java da template.jsp. Viene quindi fatto riferimento da template.jsp e tutte le variabili che espone sulla richiesta sono disponibili per l&#39;uso. Questa strategia incoraggia la separazione della logica dalla presentazione e limita la quantità di codice da copiare e incollare quando un nuovo componente viene derivato da uno esistente.

#### controller.js.jsp {#controller-js-jsp-1}

Come descritto in Modelli di pagina AEM, ogni componente può generare un frammento JavaScript per utilizzare il contenuto JSON esposto dal `data` promettere. In base alle convenzioni di Angular, un controller deve essere utilizzato solo per assegnare variabili all’ambito.

#### angular.json.jsp {#angular-json-jsp}

Questo script è incluso come frammento a livello di pagina &quot;&lt;page-name>File .angular.json&#39; esportato per ogni pagina che estende ng-page. In questo file, lo sviluppatore di componenti può esporre qualsiasi struttura JSON necessaria al componente. Nell’esempio &quot;ng-text&quot;, questa struttura include semplicemente il contenuto del testo del componente e un flag che indica se il componente include o meno testo RTF.

Il componente prodotto app per esterni Geometrixx è un esempio più complesso (/apps/geometrixx-outdoors-app/components/angular/ng-product):

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

Scarica le risorse CLI dalla console App per ottimizzarle per una piattaforma specifica e quindi crea l’app utilizzando l’API di integrazione della riga di comando (CLI, Command Line Integration) di PhoneGap. Il contenuto del file ZIP salvato nel file system locale ha la seguente struttura:

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

Si tratta di una directory nascosta che potrebbe non essere visibile a seconda delle impostazioni del sistema operativo correnti. È necessario configurare il sistema operativo in modo che questa directory sia visibile se si intende modificare gli hook dell&#39;app in essa contenuti.

#### .cordova/ganci/ {#cordova-hooks}

Questa directory contiene [Hook CLI](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/). Le cartelle nella directory degli hook contengono script node.js che vengono eseguiti nei punti esatti durante la generazione.

#### .cordova/hook/after-platform_add/ {#cordova-hooks-after-platform-add}

La directory after-platform_add contiene `copy_AMS_Conifg.js` file. Questo script copia un file di configurazione per supportare la raccolta di Adobe Mobile Services Analytics.

#### .cordova/ganci/post-preparazione/ {#cordova-hooks-after-prepare}

La directory after-Prepare contiene il `copy_resource_files.js` file. Questo script copia una serie di immagini icona e schermata iniziale in posizioni specifiche della piattaforma.

#### .cordova/hook/before_platform_add/ {#cordova-hooks-before-platform-add}

La directory before_platform_add contiene `install_plugins.js` file. Questo script esegue un’iterazione attraverso un elenco di identificatori del plug-in Cordova, installando quelli che rileva non sono già disponibili.

Questa strategia non richiede di aggregare e installare i plug-in per AEM ogni volta che Maven `content-package:install` viene eseguito il comando . La strategia alternativa per il controllo dei file nel sistema SCM richiede un bundling ripetitivo e l&#39;installazione di attività.

#### .cordova/ganci/altri ganci {#cordova-hooks-other-hooks}

Includere altri ganci come necessario. Sono disponibili i seguenti ganci (come fornito dall’app di esempio di Phonegap hello world):

* after_build
* before_build
* after_compilare
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
* after_ready
* before_ready
* after_run
* before_run

#### piattaforme/ {#platforms}

Questa directory è vuota finché non viene eseguita la `phonegap run <platform>` sul progetto. Attualmente, `<platform>` può essere `ios` o `android`.

Dopo aver creato l’app per una piattaforma specifica, viene creata la directory corrispondente che contiene il codice dell’app specifico per la piattaforma.

#### plugins/ {#plugins}

La directory dei plug-in viene compilata da ogni plug-in elencato in `.cordova/hooks/before_platform_add/install_plugins.js` dopo aver eseguito `phonegap run <platform>` comando. La directory è inizialmente vuota.

#### www. {#www}

La directory www contiene tutti i contenuti web (file HTML, JS e CSS) che implementano l’aspetto e il comportamento dell’app. Ad eccezione delle eccezioni descritte di seguito, questo contenuto proviene da AEM ed è esportato nella sua forma statica tramite Content Sync.

#### www/config.xml {#www-config-xml}

La [Documentazione di PhoneGap](https://docs.phonegap.com) fa riferimento a questo file come a un &quot;file di configurazione globale&quot;. Il file config.xml contiene molte proprietà dell&#39;app, come il nome dell&#39;app, le &#39;preferenze&#39; dell&#39;app (ad esempio se una visualizzazione web iOS consente o meno l&#39;overflow) e le dipendenze dei plug-in che sono *only* utilizzato dalla build PhoneGap.

Il file config.xml è un file statico in AEM ed è esportato così come è tramite Content Sync.

#### www/index.html {#www-index-html}

Il file index.html viene reindirizzato alla pagina iniziale dell’app.

Il file config.xml contiene il `content` elemento:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

In [la documentazione di PhoneGap](https://docs.phonegap.com), questo elemento è descritto come &quot;facoltativo &lt;content> definisce la pagina iniziale dell’app nella directory principale delle risorse web. Il valore predefinito è index.html , che di solito viene visualizzato nella directory www di livello superiore di un progetto.&quot;

La build di PhoneGap non riesce se non è presente un file index.html . Pertanto, questo file è incluso.

#### www.res {#www-res}

La directory res contiene immagini e icone della schermata iniziale. La `copy_resource_files.js` lo script copia i file nelle rispettive posizioni specifiche della piattaforma durante `after_prepare` fase di creazione.

#### www/etc {#www-etc}

Per convenzione, in AEM il nodo /etc contiene contenuto clientlib statico. La directory etc contiene le librerie Topcoat, AngularJS e Geometrixx-clientlibsall .

#### www.apps {#www-apps}

La directory delle app contiene il codice correlato alla pagina iniziale. La caratteristica unica della pagina iniziale di un’app AEM è che l’app viene inizializzata senza l’interazione dell’utente. Il contenuto clientlib (sia CSS che JS) dell’app è quindi minimo per massimizzare le prestazioni.

#### www/content {#www-content}

La directory dei contenuti contiene il resto del contenuto web dell’app. Il contenuto può includere, ma senza limitazioni, i file seguenti:

* Contenuto della pagina di HTML, creato direttamente in AEM
* Risorse immagine associate a componenti AEM
* Contenuto JavaScript generato dagli script sul lato server
* File JSON che descrivono il contenuto di una pagina o di un componente

#### www/package.json {#www-package-json}

Il file package.json è un file manifesto in cui sono elencati i file che **pieno** Il download della sincronizzazione dei contenuti include. Questo file contiene anche la marca temporale in cui è stato generato il payload di Sincronizzazione dei contenuti ( `lastModified`). Questa proprietà viene utilizzata per richiedere aggiornamenti parziali dell&#39;app da AEM.

#### www/package-update.json {#www-package-update-json}

Se questo payload è un download dell’intera app, questo manifesto contiene l’elenco esatto dei file come `package.json`.

Tuttavia, se il payload è un aggiornamento parziale, `package-update.json` contiene solo i file inclusi in questo particolare payload.

### Passaggi successivi {#the-next-steps}

Dopo aver appreso l’anatomia di un’app, consulta [Applicazioni a pagina singola](/help/mobile/phonegap-single-page-applications.md).
