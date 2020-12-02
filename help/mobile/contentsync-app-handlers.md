---
title: Gestori di app in dotazione
seo-title: Gestori di app in dotazione
description: Seguite questa pagina per informazioni sui gestori out-of-the-box per  Adobe PhoneGap Enterprise con AEM.
seo-description: Seguite questa pagina per informazioni sui gestori out-of-the-box per  Adobe PhoneGap Enterprise con AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---


# Gestori di app in dotazione{#out-of-the-box-app-handlers}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Consultate le seguenti linee guida per lo sviluppo di gestori di sincronizzazione dei contenuti:

* I gestori devono implementare *com.day.cq.contentsync.handler.ContentUpdateHandler* (direttamente o estendendo una classe che lo supporta)
* I gestori possono estendere *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Il gestore deve segnalare true solo se ha aggiornato la cache ContentSync. La segnalazione errata di true consente AEM creare un aggiornamento.
* Il gestore deve aggiornare la cache solo se il contenuto è effettivamente cambiato. Non scrivere nella cache se non è necessario un bianco ed evitare una creazione di aggiornamenti non necessaria.

## Gestori esterni {#out-of-the-box-handlers}

Di seguito sono elencati i gestori di app forniti con il prodotto:

**** mobileapppagesRendering delle pagine dell&#39;app.

* ***type - String***  - mobileapppages
* ***percorso - Stringa***  - percorso di una pagina
* ***extension - String*** - Extension da utilizzare nella richiesta. Per le pagine questo è quasi sempre *html*, ma altri sono ancora possibili.

* ***selettore - Stringa***  - Selettori opzionali separati da punto. Esempi comuni sono *touch* per il rendering delle versioni mobili di una pagina.

* ***deep - Boolean***  - Proprietà booleana opzionale che determina se includere anche le pagine figlie. Il valore predefinito è *true.*

* ***includeImages - Boolean***  - Proprietà booleana opzionale che determina se le immagini devono essere incluse. Il valore predefinito è *true*.

   * Per impostazione predefinita, sono considerati per l’inclusione solo i componenti immagine con un tipo di risorsa di base/componenti/immagine.

* ***includeVideo - Booleano***  - Proprietà booleana opzionale che determina se i video devono essere inclusi. Il valore predefinito è *true*.

* ***includeModifiedPagesOnly - Boolean***  - Se false o omesso, esegue il rendering di tutte le pagine e controlla gli aggiornamenti nel rendering. Se true, base differisce in base alle modifiche apportate a una pagina lastModified.
* ***+ riscrittura (nodo)***
   ***- relativeParentPath - String***  - il percorso in cui scrivere tutti gli altri percorsi relativi a.

>[!NOTE]
>
>Il tipo di risorsa dei componenti immagine e video interessati da questo gestore viene impostato configurando le proprietà di *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Servizio* OSGi MobilePagesUpdateHandler.

**** mobilepageassetsRaccoglie le risorse della pagina dell&#39;app.

**** mobilecontentlistElenca il contenuto del file ZIP ContentSync. Questo viene utilizzato dal client lato js sul dispositivo per eseguire la copia del file iniziale richiesta per AEM app.

Questo gestore deve essere aggiunto a qualsiasi configurazione ContentSync AEM App.

* ***type - String - mobilecontentlist***
* ***path*** - String - keep empty, must be present as a valid handler, ma il percorso viene ricavato come cache ContentSync corrente. Questo valore viene ignorato.
* ***targetRootDirectory* -**String - il prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore.
* ***order - Long* -**Order for ContentSync per eseguire questo gestore. Questo numero deve essere impostato su un valore superiore a tutti gli altri gestori, ad esempio 100. Deve essere eseguito dopo i gestori di contenuti tradizionali.

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**** mobilecontentpackageslistElenca il pacchetto di contenuto AEM in una determinata app e il serverURL a cui effettuare le richieste di aggiornamento. Viene utilizzato per richiedere gli aggiornamenti dei contenuti tramite il lato client sul dispositivo

Il gestore deve essere utilizzato nella configurazione ContentSync della shell AEM app (nodo con page-type=app-instance)

* ***type - String - mobilecontentpackageslist***
* ***path **-**String*** - Percorso di una shell app (nodo con page-type=app-instance).
* ***targetRootDirectory - String***  - il prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore.
* ***order - Long* -**Order for ContentSync per eseguire questo gestore. Questo numero deve essere impostato su un valore superiore a tutti gli altri gestori, ad esempio 100. Deve essere eseguito dopo i gestori di contenuti tradizionali.

>[!NOTE]
>
>Il seguente blocco di codice non è un&#39;implementazione esatta e deve essere utilizzato come esempio di riferimento:

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**** widgetconfigInclude un file config.xml aggiornato che unisce tutte le modifiche effettuate tramite il Centro comandi con un file config.xml fornito. Se questo gestore non è incluso, i dettagli dell&#39;app che vengono modificati tramite l&#39;interfaccia di amministrazione non saranno inclusi nella cache.

Questo handler deve essere utilizzato in una configurazione AEM App Shell ContentSync (nodo con page-type=[app-instance]).

* ***tipo - String* - **widgetconfig
* ***path **-**String*** - Percorso di qualsiasi nodo secondario della shell dell&#39;app (nodo con page-type=[app-instance]).
* ***targetRootDirectory - String***  - il prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore.
* ***targetIconDirectory - String*** - la directory in cui inserire le icone per l&#39;app

**** mobileADBMobileConfigJSONInclude il file ADBMobileConfig.JSON se il servizio cloud AMS è stato configurato.

Questo viene utilizzato in fase di compilazione per configurare il plugin AMS per il supporto analitico.

Il gestore deve essere utilizzato nella configurazione ContentSync della shell AEM app (nodo con page-type=app-instance)

* ***type - String*** - mobileADBMobileConfigJSON
* ***percorso - Stringa***  - Percorso di una shell app (nodo con page-type=app-instance o una RT che estende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String***  - il prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore

**** notifiche sconfigExtracts configurazioni di notifiche richieste sul dispositivo. Le proprietà vengono estratte dalla rispettiva configurazione del servizio cloud del servizio push associata all&#39;app.

Le proprietà non AEM nel nodo jcr:content del servizio cloud vengono estratte e aggiunte al file **page-notifications-config.json** JSON da includere nel file www root dell&#39;app del contenuto.

AEM proprietà sono quelle con spazio dei nomi con &quot;cq&quot;, &quot;sling&quot; o &quot;jcr&quot;. È possibile escludere altre proprietà utilizzando la proprietà &quot;excludeProperties&quot; nel nodo di configurazione della sincronizzazione dei contenuti.

* ***type - String***  - notificationsconfig
* ***excludeProperties - String[]*** - proprietà da escludere

**** contentsyncconfigcontentRaccoglie il contenuto da una configurazione ContentSync esistente.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Percorso di uno dei seguenti:

   * un&#39;altra configurazione ContentSync
   * a un pacchetto di contenuti (verrà utilizzata la proprietà phonegap-exportTemplate per trovare la configurazione ContentSync)
   * a una risorsa mobile (i contenuti dell’app si trovano in tale risorsa e, se i pacchetti di contenuto dispongono di una proprietà page-includeInBuild che è true, il phonegap-exportTemplate verrà utilizzato per trovare la configurazione ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - se true, creare un  **** aggiornamento iniziale nella configurazione di destinazione prima dell&#39;importazione, se una volta non esiste già

* ***autoFillBeforeImport - Boolean***  - se true, aggiorna/compila la configurazione di destinazione prima di importare
* ***configSuffix - String*** - una stringa da aggiungere al percorso indicato nella proprietà &quot;phonegap-exportTemplate&quot; di app-content. Questo può essere utilizzato per distinguere diversi modelli di esportazione. Ad esempio, questa proprietà può essere impostata su **&quot;-dev&quot;** per indicare che è necessario utilizzare *&quot;/../../../appconfig-dev&quot;* (anziché *&quot;/.././../appconfig&quot;*).

**app-** assetsInclude tutte le risorse associate a un&#39;istanza dell&#39;app. Questo handler includerà tutte le risorse trovate nel percorso specificato insieme alle risorse a cui fa riferimento la proprietà appAssetPath di un&#39;istanza dell&#39;app.

* ***type - String*** - app-assets

* ***percorso **-**Stringa***  - percorso di una posizione in un&#39;istanza di app in cui sono memorizzate le risorse dell&#39;app

**** mobileappoffersÈ stato introdotto un nuovo gestore di sincronizzazione dei contenuti per il caso d’uso Personalizzazione per il rendering del contenuto di destinazione. Il gestore &#39;mobileappoffers&#39; è in grado di eseguire il rendering delle offerte di destinazione associate create dall&#39;autore del contenuto. Il gestore mobileappoffers estende il gestore di aggiornamenti delle pagine astratte, pertanto molte delle proprietà sono simili. I dettagli del gestore mobileappoffers hanno le seguenti proprietà.

Il gestore mobileappsoffers estende il gestore mobileappspages e aggiunge le seguenti proprietà:

* ***locationRoot - String***  - specifica la posizione dell&#39;applicazione mobile
* ***includePageTypes - String***  - default per supportare cq/personalization/components/teaserpage e cq/personalization/components/offerproxy
* ***selector - String*** - deve essere impostato su tandt
* ***path - String*** - il percorso del marchio della campagna

**** mobileappconfigIl gestore di sincronizzazione del contenuto mobileappconfig fornisce un modo per inserire i dati JSON in MobileAppsConfig.json. Per registrare una classe di provider, gli sviluppatori aggiungeranno la classe MobileAppsInfoProvider all&#39;elenco dei provider. Il gestore eseguirà un&#39;iterazione sull&#39;elenco di MobileAppsInfoProviders e consentirà al provider di inserire i dati nel file json risultante. L&#39;elenco delle proprietà supportate da questo gestore è:

* ***path **-**String*** - il percorso di un nodo di istanza dell&#39;app con pge-type=app-instance o un RT che si estende /libs/mobileapps/core/components/instance
* ***provider - Stringa*** `[]`  - elenco di MobileAppsInfoProviders completi
* ***targetRootDirectory - String*** - la directory in cui scrivere il file MobileAppsConfig.json.
* **fileName - String**  - nome facoltativo del file in cui scrivere il file JSON, per impostazione predefinita è MobileAppsConfig.json

È possibile che più gestori mobileappconfig siano configurati ciascuno con un set univoco di provider che scrivono in file JSON diversi.

### Verifica dei gestori di sincronizzazione dei contenuti {#testing-content-sync-handlers}

**Passaggi per il controllo della cache** IntegrityClear

* Cancella cache
* Eseguire il gestore (cache aggiornata)
* Eseguire nuovamente il gestore (la cache non deve essere aggiornata)

**Passaggi per il debug**

* Eseguire la configurazione
* Esportare la configurazione o la revisione sul dispositivo
* Se il rendering non riesce, controllare se mancano *stili/risorse/libs* o controllare se sono presenti percorsi non validi per *stili/risorse/libs*

**** LoggingAbilita la registrazione di debug di ContentSync tramite le configurazioni di logger OSGI sul pacchetto  `com.day.cq.contentsync` Questo consente di tenere traccia dei gestori eseguiti e se hanno aggiornato la cache e segnalato l&#39;aggiornamento della cache.

## Risorse aggiuntive {#additional-resources}

Per informazioni su ruoli e responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Authoring per  Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per  Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Per iniziare a sviluppare  app AEM Mobile, fai clic su [qui](/help/mobile/getting-started-aem-mobile.md).

