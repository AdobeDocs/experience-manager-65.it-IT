---
title: Gestori di app integrati
seo-title: Out of the Box App Handlers
description: Segui questa pagina per scoprire i gestori predefiniti di Adobe PhoneGap Enterprise con AEM.
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# Gestori di app integrati{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Consulta le seguenti linee guida per lo sviluppo dei gestori di sincronizzazione dei contenuti:

* I gestori devono implementare *com.day.cq.contentsync.handler.ContentUpdateHandler* (direttamente o estendendo una classe che lo fa)
* I gestori possono estendere *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Il gestore deve segnalare true solo se ha aggiornato la cache ContentSync. La segnalazione errata su true consente AEM creare un aggiornamento.
* Il gestore deve aggiornare la cache solo se il contenuto è effettivamente cambiato. Non scrivere nella cache se non è necessario un bianco ed evita una creazione di aggiornamenti non necessaria.

## Gestori esterni {#out-of-the-box-handlers}

Di seguito sono elencati i gestori di app pronti all’uso:

**mobileapppages** Esegue il rendering delle pagine delle app.

* ***type - String*** - mobileapppages
* ***path - String*** - percorso di una pagina
* ***estensione - Stringa*** - Estensione da utilizzare nella richiesta. Per le pagine questo è quasi sempre *html* Ma altri sono ancora possibili.

* ***selettore - Stringa*** - Selettori opzionali separati da punto. Esempi comuni *tocco* per il rendering delle versioni mobili di una pagina.

* ***deep - Boolean*** - Proprietà booleana opzionale che determina se includere anche le pagine figlie. Il valore predefinito è *vero.*

* ***includeImages - Booleano*** - Proprietà booleana opzionale che determina se le immagini devono essere incluse. Il valore predefinito è *true*.

   * Per impostazione predefinita, sono considerati per l’inclusione solo i componenti immagine con un tipo di risorsa foundation/components/image.

* ***includeVideos - Booleano*** - Proprietà booleana opzionale determinare se i video devono essere inclusi. Il valore predefinito è *true*.

* ***includeModifiedPagesOnly - Booleano*** - Se false o omesso, esegue il rendering di tutte le pagine e controlla gli aggiornamenti nel rendering. Se true, base differisce dalle modifiche apportate a una pagina lastModified.
* ***+ riscrittura (nodo)***
   ***- relativeParentPath - String*** - il percorso di scrittura di tutti gli altri percorsi relativi a.

>[!NOTE]
>
>Il tipo di risorsa dei componenti immagine e video interessati da questo gestore viene impostato configurando le proprietà del *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Servizio OSGi MobilePagesUpdateHandler*.

**mobilepageassets** Raccoglie le risorse della pagina dell&#39;app.

**mobilecontentlisting** Elenca il contenuto dello zip ContentSync. Questo viene utilizzato da js lato client sul dispositivo per eseguire la copia iniziale del file richiesta per AEM app.

Questo gestore deve essere aggiunto a qualsiasi configurazione ContentSync AEM Apps.

* ***type - String - mobilecontentlisting***
* ***path*** - Stringa - mantieni vuoto, deve essere presente per essere visto come un gestore valido, ma il percorso è dedotto per essere la cache ContentSync corrente. Questo valore viene ignorato.
* ***targetRootDirectory* -**Stringa: il prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore.
* ***order - Long* -**Ordine per ContentSync di eseguire questo gestore. Questo numero deve essere impostato più alto di tutti gli altri gestori, ad esempio 100. Deve essere eseguito dopo i gestori di contenuti tradizionali.

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

**mobilecontentpackageslisting** Elenca il pacchetto di contenuto AEM in una determinata app e il serverURL a cui effettuare le richieste di aggiornamento. Viene utilizzato il js lato client sul dispositivo per richiedere aggiornamenti del contenuto

Il gestore deve essere utilizzato nella configurazione AEM App Shell ContentSync (nodo con page-type=app-instance)

* ***type - String - mobilecontentpackageslisting***
* ***path **-**Stringa*** - Percorso di una shell di app (nodo con page-type=app-instance).
* ***targetRootDirectory - String*** - il prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore.
* ***order - Long* -**Ordine per ContentSync per eseguire questo gestore. Questo numero deve essere impostato più alto di tutti gli altri gestori, ad esempio 100. Deve essere eseguito dopo i gestori di contenuti tradizionali.

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

**widgetconfig** Include un file config.xml aggiornato che unisce tutte le modifiche effettuate tramite il Centro comandi con un file config.xml fornito. Se questo gestore non è incluso, i dettagli dell’app modificati tramite l’interfaccia di amministrazione non verranno inclusi nella cache.

Questo gestore deve essere utilizzato su una configurazione AEM App Shell ContentSync (nodo con page-type=)[app-istanza]).

* ***type - String* - **widgetconfig
* ***path **-**Stringa*** - Percorso di qualsiasi nodo figlio della shell dell&#39;app (nodo con page-type=[app-istanza]).
* ***targetRootDirectory - String*** - il prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore.
* ***targetIconDirectory - String*** - la directory in cui inserire le icone dell’app

**mobileADBMobileConfigJSON** Includi il file ADBMobileConfig.JSON se il servizio cloud AMS è stato configurato.

Viene utilizzato in fase di compilazione per configurare il plug-in AMS per il supporto analitico.

Il gestore deve essere utilizzato nella configurazione AEM App Shell ContentSync (nodo con page-type=app-instance)

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** - Percorso di una shell di app (nodo con pge-type=app-instance o un RT che estende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String*** - il prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore

**notificationsconfig** Estrae le configurazioni di notifica richieste sul dispositivo. Le proprietà vengono estratte dalla rispettiva configurazione del servizio cloud di servizi push associata all’app.

Le proprietà non AEM nel nodo jcr:content del servizio cloud vengono estratte e aggiunte al **pge-notifications-config.json** File JSON da includere nella directory principale www del contenuto dell’app.

AEM proprietà sono quelle con spazio dei nomi con &quot;cq&quot;, &quot;sling&quot; o &quot;jcr&quot;. Altre proprietà possono essere escluse utilizzando la proprietà &quot;excludeProperties&quot; sul nodo di configurazione della sincronizzazione del contenuto.

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]*** - proprietà da escludere

**contentsyncconfigcontent** Raccoglie il contenuto da una configurazione ContentSync esistente.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Percorso a uno dei seguenti percorsi:

   * un&#39;altra configurazione ContentSync
   * a un pacchetto di contenuti (utilizzerà la proprietà phonegap-exportTemplate per trovare la configurazione ContentSync)
   * in una risorsa mobile (i contenuti dell&#39;app si trovano sotto tale risorsa e, se tali pacchetti di contenuto hanno una proprietà page-includeInBuild che è true, il phonegap-exportTemplate verrà utilizzato per trovare la relativa configurazione ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - se true, crea un **update** nella configurazione di destinazione prima dell’importazione, se una volta non esiste già

* ***autoFillBeforeImport - Boolean*** - se true, aggiorna/compila la configurazione di destinazione prima dell&#39;importazione
* ***configSuffix - String*** - una stringa da aggiungere al percorso indicato nella proprietà &quot;phonegap-exportTemplate&quot; di app-content. Può essere utilizzato per distinguere diversi modelli di esportazione. Ad esempio, questa proprietà può essere impostata su **&quot;-dev&quot;** indicare che *&quot;/../../../appconfig-dev&quot;* devono essere utilizzati (anziché *&quot;/.././../appconfig&quot;*).

**app-assets** Include tutte le risorse associate a un&#39;istanza dell&#39;app. Questo gestore includerà tutte le risorse presenti nel percorso specificato, insieme a tutte le risorse a cui fa riferimento la proprietà appAssetPath di un&#39;istanza dell&#39;app.

* ***type - String*** - app-assets

* ***path **-**Stringa*** - percorso di una posizione in un&#39;istanza dell&#39;app in cui sono memorizzate le risorse dell&#39;app

**telefonatori** È stato introdotto un nuovo gestore di sincronizzazione dei contenuti per il caso d’uso Personalizzazione per eseguire il rendering del contenuto di destinazione. Il gestore &quot;mobileappoffers&quot; sa come eseguire il rendering delle offerte target associate create dall’autore del contenuto. Il gestore mobileappoffers estende il gestore di aggiornamenti delle pagine astratte, pertanto molte delle proprietà sono simili. I dettagli del gestore mobileappoffer hanno le seguenti proprietà.

Il gestore mobileappsoffers estende il gestore mobileappspages e aggiunge le seguenti proprietà:

* ***locationRoot - String*** - specificare la posizione dell&#39;app mobile
* ***includePageTypes - String*** - impostazioni predefinite per supportare cq/personalization/components/teaserpage e cq/personalization/components/offerproxy
* ***selettore - Stringa*** - deve essere impostato su standard
* ***path - String***- il percorso del marchio della campagna

**mobileappconfig** Il gestore di sincronizzazione del contenuto mobileappconfig fornisce un modo per inserire dati JSON in MobileAppsConfig.json. Per registrare una classe di provider, gli sviluppatori aggiungeranno la classe MobileAppsInfoProvider con l’elenco dei provider. Il gestore eseguirà l’iterazione sull’elenco di MobileAppsInfoProviders e consentirà al provider di inserire i dati nel file json risultante. L&#39;elenco delle proprietà supportate da questo gestore è:

* ***path **-**Stringa*** - il percorso di un nodo di istanza dell&#39;app con pge-type=app-instance o un RT che estende /libs/mobileapps/core/components/instance
* ***provider - String*** `[]` - Elenco di MobileAppsInfoProviders completamente qualificati
* ***targetRootDirectory - String*** - la directory in cui scrivere il file MobileAppsConfig.json.
* **fileName - String** - nome facoltativo del file in cui scrivere il JSON, impostazione predefinita MobileAppsConfig.json

È possibile che più gestori mobileappconfig siano configurati ciascuno con un set univoco di provider che scrivono in file JSON diversi.

### Verifica dei gestori di sincronizzazione dei contenuti {#testing-content-sync-handlers}

**Passaggi per il controllo dell’integrità** Cancella cache

* Cancella cache
* Esegui il tuo handler (cache aggiornata)
* Esegui di nuovo il gestore (la cache non deve essere aggiornata)

**Passaggi per il debug**

* Esegui la configurazione
* Esporta la configurazione o la revisione sul dispositivo
* Se il rendering non riesce, verifica che manca *stili/risorse/libs* o controlla i percorsi errati in *stili/risorse/libs*

**Registrazione** Abilita la registrazione di debug ContentSync tramite le configurazioni del logger OSGI sul pacchetto `com.day.cq.contentsync` Questo ti consente di monitorare l’esecuzione dei gestori e se hanno aggiornato la cache e segnalato l’aggiornamento della cache.

## Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e le responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Authoring per Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Per iniziare a sviluppare un’app AEM Mobile, fai clic su [qui](/help/mobile/getting-started-aem-mobile.md).
