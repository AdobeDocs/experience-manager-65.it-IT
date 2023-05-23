---
title: Gestori di app pronti all’uso
seo-title: Out of the Box App Handlers
description: Segui questa pagina per scoprire i gestori predefiniti per Adobe PhoneGap Enterprise con AEM.
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

# Gestori di app pronti all’uso{#out-of-the-box-app-handlers}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Consulta le seguenti linee guida per lo sviluppo di gestori di sincronizzazione dei contenuti:

* I gestori devono implementare *com.day.cq.contentsync.handler.ContentUpdateHandler* (direttamente o estendendo una classe che lo fa)
* I gestori possono estendere *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Il gestore deve segnalare true solo se ha aggiornato la cache di ContentSync. Segnalare falsamente true consentirà al AEM di creare un aggiornamento.
* Il gestore deve aggiornare la cache solo se il contenuto è stato effettivamente modificato. Non scrivere nella cache se non è necessario un bianco ed evita di creare un aggiornamento non necessario.

## Gestori pronti all’uso {#out-of-the-box-handlers}

Di seguito sono elencati i gestori di app predefiniti:

**mobileapppages** Esegue il rendering delle pagine dell&#39;app.

* ***type - String*** - mobileapppages
* ***path - String*** : percorso di una pagina
* ***extension - String*** - Estensione da utilizzare nella richiesta. Per le pagine questo è quasi sempre *html*, ma altri sono ancora possibili.

* ***selettore - Stringa*** - Selettori opzionali separati da un punto. Esempi comuni sono *tocco* per il rendering delle versioni mobili di una pagina.

* ***deep - Boolean*** - Proprietà booleana opzionale che determina se includere o meno le pagine figlie. Il valore predefinito è *vero.*

* ***includeImages - Boolean*** - Proprietà booleana opzionale che determina se le immagini devono essere incluse. Il valore predefinito è *true*.

   * Per impostazione predefinita, solo i componenti immagine con un tipo di risorsa fondazione/componenti/immagine vengono considerati per l’inclusione.

* ***includeVideos - Booleano*** - Proprietà booleana opzionale che determina se i video devono essere inclusi. Il valore predefinito è *true*.

* ***includeModifiedPagesOnly - Boolean*** : se false o omesso, esegui il rendering di tutte le pagine e controlla gli aggiornamenti nel rendering. Se true, base differisce in base alle modifiche apportate a una pagina lastModified.
* ***+ riscrittura (nodo)***
   ***- relativeParentPath - Stringa*** : il percorso per scrivere tutti gli altri percorsi relativi a.

>[!NOTE]
>
>Il tipo di risorsa dei componenti immagine e video interessati da questo gestore viene impostato configurando le proprietà del *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Servizio OSGi MobilePagesUpdateHandler*.

**mobilepageassets** Raccoglie le risorse della pagina dell&#39;app.

**mobilecontentlisting** Elenca il contenuto dello zip ContentSync. Viene utilizzato dal js lato client sul dispositivo per eseguire la copia iniziale del file necessaria per le app AEM.

Questo gestore deve essere aggiunto a qualsiasi configurazione di ContentSync per app AEM.

* ***type - String - mobilecontentlisting***
* ***percorso*** - Stringa - mantieni vuoto, deve essere presente per essere visto come un gestore valido, ma si deduce che il percorso sia la cache ContentSync corrente. Questo valore viene ignorato.
* ***targetRootDirectory* -**Stringa: il prefisso da aggiungere ai percorsi come directory principale di destinazione per l’aggiornamento del contenuto per questo gestore.
* ***order - Long* -**Ordina ContentSync per eseguire questo gestore. Questo numero deve essere impostato su un valore superiore a tutti gli altri gestori, ad esempio 100. Deve essere eseguito dopo i gestori di contenuti tradizionali.

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

**mobilecontentpackageslisting** Elenca il pacchetto di contenuti AEM in una determinata app e l’URL del server a cui inviare le richieste di aggiornamento. Viene utilizzato da JS lato client sul dispositivo per richiedere aggiornamenti del contenuto

Il gestore deve essere utilizzato nella configurazione ContentSync della shell dell’app AEM (nodo con pge-type=app-instance)

* ***type - String - mobilecontentpackageslisting***
* ***percorso **-**Stringa*** : percorso di una shell dell’app (nodo con pge-type=app-instance).
* ***targetRootDirectory - Stringa*** : prefisso da aggiungere ai percorsi come directory principale di destinazione per l’aggiornamento del contenuto per questo gestore.
* ***order - Long* -**Ordinare a ContentSync di eseguire questo gestore. Questo numero deve essere impostato su un valore superiore a tutti gli altri gestori, ad esempio 100. Deve essere eseguito dopo i gestori di contenuti tradizionali.

>[!NOTE]
>
>Il seguente blocco di codice non è un’implementazione esatta e deve essere utilizzato come esempio di riferimento:

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

**widgetconfig** Include un file config.xml aggiornato che unisce tutte le modifiche apportate tramite il centro comandi con un file config.xml fornito. Se questo gestore non è incluso, i dettagli dell’app modificati tramite l’interfaccia di amministrazione non verranno inclusi nella cache.

Questo gestore deve essere utilizzato in una configurazione ContentSync della shell dell’app AEM (nodo con pge-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***percorso **-**Stringa*** : percorso di qualsiasi nodo figlio della shell dell’app (nodo con pge-type=[app-instance]).
* ***targetRootDirectory - Stringa*** : prefisso da aggiungere ai percorsi come directory principale di destinazione per l’aggiornamento del contenuto per questo gestore.
* ***targetIconDirectory - Stringa*** : la directory in cui inserire le icone per l’app

**mobileADBMobileConfigJSON** Includi il file ADBMobileConfig.JSON se è stato configurato il servizio cloud AMS.

Viene utilizzato in fase di compilazione per configurare il plug-in AMS per il supporto analitico.

Il gestore deve essere utilizzato nella configurazione ContentSync della shell dell’app AEM (nodo con pge-type=app-instance)

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** : percorso di una shell dell’app (nodo con pge-type=app-instance o RT che estende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - Stringa*** : prefisso da aggiungere ai percorsi come directory principale di destinazione per l’aggiornamento del contenuto per questo gestore

**notificationsconfig** Estrae le configurazioni di notifica necessarie sul dispositivo. Le proprietà vengono estratte dalla rispettiva configurazione del servizio cloud del servizio push associata all’app.

Le proprietà non AEM nel nodo jcr:content del servizio cloud vengono estratte e aggiunte al **pge-notifications-config.json** File JSON da includere nella directory principale www del contenuto dell’app.

Le proprietà dell’AEM sono quelle con spazio dei nomi tra &quot;cq&quot;, &quot;sling&quot; o &quot;jcr&quot;. Altre proprietà possono essere escluse utilizzando la proprietà &quot;excludeProperties&quot; nel nodo di configurazione content-sync.

* ***type - String*** - notificationsconfig
* ***excludeProperties - Stringa[]*** - proprietà da escludere

**contentsyncconfigcontent** Raccoglie contenuto da una configurazione ContentSync esistente.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Percorso di uno dei seguenti elementi:

   * un&#39;altra configurazione ContentSync
   * in un pacchetto di contenuti (utilizzerà la proprietà phonegap-exportTemplate per trovare la relativa configurazione ContentSync)
   * a una risorsa mobile (i contenuti dell’app si trovano sotto tale risorsa e, se tali pacchetti di contenuto hanno una proprietà page-includeInBuild che è true, phonegap-exportTemplate verrà utilizzato per trovare la relativa configurazione ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Booleano*** - se true, crea una **aggiorna** nella configurazione di destinazione prima dell’importazione se una volta non esiste già

* ***autoFillBeforeImport - Booleano*** - se true, aggiorna/compila la configurazione di destinazione prima dell’importazione
* ***configSuffix - Stringa*** : stringa da aggiungere al percorso indicato nella proprietà &quot;phonegap-exportTemplate&quot; di app-content. Questa può essere utilizzata per distinguere diversi modelli di esportazione. Ad esempio, questa proprietà può essere impostata su **&quot;-dev&quot;** per indicare che *&quot;/../../../appconfig-dev&quot;* devono essere utilizzati (anziché *&quot;/../../../appconfig&quot;*).

**app-assets** Include tutte le risorse associate a un&#39;istanza di app. Questo gestore includerà tutte le risorse trovate nel percorso specificato, insieme a tutte le risorse a cui fa riferimento la proprietà appAssetPath di un&#39;istanza di app.

* ***type - String*** - app-assets

* ***percorso **-**Stringa*** : percorso di un&#39;istanza dell&#39;app in cui sono memorizzate le risorse dell&#39;app

**mobileapffffers** È stato introdotto un nuovo gestore di sincronizzazione dei contenuti per il caso di utilizzo Personalizzazione per eseguire il rendering di contenuti di destinazione. Il gestore &quot;mobileapffers&quot; è in grado di eseguire il rendering delle offerte target associate create dall’autore di contenuto. Il gestore mobileapffers estende il gestore di aggiornamento delle pagine astratte, pertanto molte delle proprietà sono simili. I dettagli del gestore mobileappoffers hanno le seguenti proprietà.

Il gestore mobileappofferers estende il gestore mobileappspages e aggiunge le seguenti proprietà:

* ***locationRoot - Stringa*** - specificare la posizione dell&#39;app mobile
* ***includePageTypes - Stringa*** : impostazioni predefinite per il supporto di cq/personalization/components/teaserpage e cq/personalization/components/offerproxy
* ***selettore - Stringa*** - deve essere impostato su tandt
* ***path - String***- il percorso verso il marchio della campagna

**mobileappconfig** Il gestore di sincronizzazione del contenuto mobileappconfig consente di inserire dati JSON in MobileAppsConfig.json. Per registrare una classe provider, gli sviluppatori aggiungeranno la classe MobileAppsInfoProvider all&#39;elenco dei provider. Il gestore scorre l’elenco di MobileAppsInfoProviders e consente al provider di inserire dati nel file json risultante. L&#39;elenco delle proprietà supportate dal gestore è:

* ***percorso **-**Stringa*** : percorso di un nodo di istanza app con pge-type=app-instance o un RT che estende /libs/mobileapps/core/components/instance
* ***provider - Stringa*** `[]` - l&#39;elenco di MobileAppsInfoProvider completi
* ***targetRootDirectory - Stringa*** : la directory in cui scrivere il file MobileAppsConfig.json.
* **fileName - Stringa** : nome opzionale del file in cui scrivere il JSON; l’impostazione predefinita è MobileAppsConfig.json

È possibile configurare più gestori mobileappconfig ciascuno con un set univoco di provider che scrivono in file JSON diversi.

### Verifica dei gestori di sincronizzazione dei contenuti {#testing-content-sync-handlers}

**Passaggi per la verifica dell&#39;integrità** Cancella cache

* Cancella cache
* Eseguire il gestore (cache aggiornata)
* Esegui nuovamente il gestore (la cache non deve essere aggiornata)

**Passaggi per il debug**

* Eseguire la configurazione
* Esportare la configurazione o la revisione sul dispositivo
* Se il rendering non riesce, verifica se è mancante *stili/risorse/libs* o verifica la presenza di percorsi non validi per *stili/risorse/libs*

**Registrazione** Abilitare la registrazione di debug di ContentSync tramite le configurazioni del logger OSGI sul pacchetto `com.day.cq.contentsync` Questo consente di tenere traccia di quali gestori hanno eseguito e se hanno aggiornato la cache e segnalato l’aggiornamento della cache.

## Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e sulle responsabilità di un amministratore e di uno sviluppatore, consulta le risorse seguenti:

* [Authoring per Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Per iniziare a sviluppare app AEM Mobile, fai clic su [qui](/help/mobile/getting-started-aem-mobile.md).
