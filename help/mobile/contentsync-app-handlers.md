---
title: Gestori di app pronti all’uso
description: Segui questa pagina per scoprire i gestori predefiniti per Adobe PhoneGap Enterprise con AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1408'
ht-degree: 0%

---

# Gestori di app pronti all’uso{#out-of-the-box-app-handlers}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Consulta le seguenti linee guida per lo sviluppo di gestori di sincronizzazione dei contenuti:

* I gestori devono implementare *com.day.cq.contentsync.handler.ContentUpdateHandler* (direttamente o estendendo una classe che esegue)
* I gestori possono estendere *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Il gestore deve segnalare true solo se ha aggiornato la cache di ContentSync. Segnalare falsamente true consentirà al AEM di creare un aggiornamento.
* Il gestore deve aggiornare la cache solo se il contenuto è stato effettivamente modificato. Non scrivere nella cache se non è necessario un bianco ed evita di creare un aggiornamento non necessario.

## Gestori pronti all’uso {#out-of-the-box-handlers}

Di seguito sono elencati i gestori di app predefiniti:

**mobileapppages** Esegue il rendering delle pagine dell&#39;app.

* ***tipo - Stringa*** - mobileapppages
* ***percorso - Stringa*** - percorso di una pagina
* ***estensione - Stringa*** - Estensione da utilizzare nella richiesta. Per le pagine si tratta quasi sempre di *html*, ma altri sono ancora possibili.

* ***selettore - Stringa*** - Selettori facoltativi separati da un punto. Esempi comuni sono *touch* per il rendering delle versioni mobili di una pagina.

* ***deep - Boolean*** - Proprietà booleana opzionale che determina se includere anche le pagine figlie. Il valore predefinito è *true.*

* ***includeImages - Booleano*** - Proprietà booleana opzionale che determina se le immagini devono essere incluse. Il valore predefinito è *true*.

   * Per impostazione predefinita, solo i componenti immagine con un tipo di risorsa fondazione/componenti/immagine vengono considerati per l’inclusione.

* ***includeVideos - Booleano*** - La proprietà booleana opzionale determina se i video devono essere inclusi. Il valore predefinito è *true*.

* ***includeModifiedPagesOnly - Booleano*** - Se false o omesse, esegui il rendering di tutte le pagine e controlla gli aggiornamenti nel rendering. Se true, base differisce in base alle modifiche apportate a una pagina lastModified.
* ***+ riscrittura (nodo)***
  ***- relativeParentPath - String*** - percorso per la scrittura di tutti gli altri percorsi relativi a.

>[!NOTE]
>
>Il tipo di risorsa dei componenti immagine e video interessati da questo gestore viene impostato configurando le proprietà di *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Servizio OSGi MobilePagesUpdateHandler*.

**mobilepageassets** Raccoglie le risorse della pagina dell&#39;app.

**mobilecontentlisting** Elenca il contenuto del file zip ContentSync. Viene utilizzato dal js lato client sul dispositivo per eseguire la copia iniziale del file necessaria per le app AEM.

Questo gestore deve essere aggiunto a qualsiasi configurazione di ContentSync per app AEM.

* ***tipo - Stringa - mobilecontentlisting***
* ***percorso*** - Stringa - mantieni vuoto, deve essere presente per essere visualizzato come un gestore valido, ma si deduce che il percorso sia la cache ContentSync corrente. Questo valore viene ignorato.
* ***targetRootDirectory* -**Stringa - Prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore.
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

**mobilecontentpackageslisting** Elenca il pacchetto di contenuti AEM in una determinata app e l&#39;URL del server a cui inviare le richieste di aggiornamento. Viene utilizzato da JS lato client sul dispositivo per richiedere aggiornamenti del contenuto

Il gestore deve essere utilizzato nella configurazione ContentSync della shell dell’app AEM (nodo con pge-type=app-instance)

* ***tipo - Stringa - mobilecontentpackageslisting***
* ***percorso **-**Stringa*** - Percorso di una shell app (nodo con pge-type=app-instance).
* ***targetRootDirectory - Stringa*** - Prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore.
* ***order - Long* -**Order for ContentSync per eseguire questo gestore. Questo numero deve essere impostato su un valore superiore a tutti gli altri gestori, ad esempio 100. Deve essere eseguito dopo i gestori di contenuti tradizionali.

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

**widgetconfig** Include un file config.xml aggiornato che unisce eventuali modifiche apportate tramite il centro comandi con un file config.xml fornito. Se questo gestore non è incluso, i dettagli dell’app modificati tramite l’interfaccia di amministrazione non verranno inclusi nella cache.

Questo gestore deve essere utilizzato in una configurazione ContentSync della shell dell&#39;app AEM (nodo con pge-type=[app-instance]).

* ***tipo - Stringa* - **widgetconfig
* ***percorso **-**Stringa*** - Percorso di qualsiasi nodo figlio della shell dell&#39;app (nodo con pge-type=[app-instance]).
* ***targetRootDirectory - Stringa*** - Prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore.
* ***targetIconDirectory - Stringa*** - Directory in cui inserire le icone per l&#39;app

**mobileADBMobileConfigJSON** Includi il file ADBMobileConfig.JSON se il servizio cloud AMS è stato configurato.

Viene utilizzato in fase di compilazione per configurare il plug-in AMS per il supporto analitico.

Il gestore deve essere utilizzato nella configurazione ContentSync della shell dell’app AEM (nodo con pge-type=app-instance)

* ***tipo - Stringa*** - mobileADBMobileConfigJSON
* ***percorso - Stringa*** - Percorso di una shell dell&#39;app (nodo con pge-type=app-instance o RT che estende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - Stringa*** - Prefisso da aggiungere ai percorsi come radice di destinazione per l&#39;aggiornamento del contenuto per questo gestore

**notificationsconfig** Estrae le configurazioni delle notifiche necessarie sul dispositivo. Le proprietà vengono estratte dalla rispettiva configurazione del servizio cloud del servizio push associata all’app.

Le proprietà non AEM nel nodo jcr:content del servizio cloud vengono estratte e aggiunte al file JSON **pge-notifications-config.json** per l&#39;inclusione nella directory principale www del contenuto dell&#39;app.

Le proprietà dell’AEM sono quelle con spazio dei nomi tra &quot;cq&quot;, &quot;sling&quot; o &quot;jcr&quot;. Altre proprietà possono essere escluse utilizzando la proprietà &quot;excludeProperties&quot; nel nodo di configurazione content-sync.

* ***type - String*** - notificationsconfig
* ***excludeProperties - Stringa[]*** - proprietà da escludere

**contentsyncconfigcontent** Raccoglie contenuto da una configurazione ContentSync esistente.

* ***type - String*** - contentsyncconfigcontent
* ***percorso - Stringa*** - Percorso di uno dei seguenti elementi:

   * un&#39;altra configurazione ContentSync
   * in un pacchetto di contenuti (utilizzerà la proprietà phonegap-exportTemplate per trovare la relativa configurazione ContentSync)
   * a una risorsa mobile (i contenuti dell’app si trovano sotto tale risorsa e, se tali pacchetti di contenuto hanno una proprietà page-includeInBuild che è true, phonegap-exportTemplate viene utilizzato per trovare la relativa configurazione ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Booleano*** - se true, creare un **aggiornamento** iniziale nella configurazione di destinazione prima dell&#39;importazione se non esiste già una volta

* ***autoFillBeforeImport - Booleano*** - se true, aggiorna/compila la configurazione di destinazione prima dell&#39;importazione
* ***configSuffix - Stringa*** - Stringa da aggiungere al percorso indicato nella proprietà &quot;phonegap-exportTemplate&quot; di app-content. Questa può essere utilizzata per distinguere diversi modelli di esportazione. Ad esempio, questa proprietà può essere impostata su **&quot;-dev&quot;** per indicare che deve essere utilizzato *&quot;/../../../appconfig-dev&quot;* (anziché *&quot;/../../../appconfig&quot;*).

**app-assets** include tutte le risorse associate a un&#39;istanza dell&#39;app. Questo gestore includerà tutte le risorse trovate nel percorso specificato, insieme a tutte le risorse a cui fa riferimento la proprietà appAssetPath di un&#39;istanza di app.

* ***tipo - Stringa*** - risorse-app

* ***percorso **-**Stringa*** - percorso in un&#39;istanza dell&#39;app in cui sono archiviate le risorse dell&#39;app

**mobileappoffers** È stato introdotto un nuovo gestore di sincronizzazione dei contenuti per il caso d&#39;uso Personalization per il rendering del contenuto di destinazione. Il gestore &quot;mobileapffers&quot; è in grado di eseguire il rendering delle offerte target associate create dall’autore di contenuto. Il gestore mobileapffers estende il gestore di aggiornamento delle pagine astratte, pertanto molte delle proprietà sono simili. I dettagli del gestore mobileappoffers hanno le seguenti proprietà.

Il gestore mobileappofferers estende il gestore mobileappspages e aggiunge le seguenti proprietà:

* ***locationRoot - String*** - specifica il percorso dell&#39;app mobile
* ***includePageTypes - Stringa*** - supporta per impostazione predefinita cq/personalization/components/teaserpage e cq/personalization/components/offerproxy
* ***selettore - Stringa*** - deve essere impostato su tandt
* ***percorso - Stringa***- Percorso del marchio della campagna

**mobileappconfig** Il gestore di sincronizzazione del contenuto mobileappconfig consente di inserire dati JSON in MobileAppsConfig.json. Per registrare una classe provider, gli sviluppatori aggiungeranno la classe MobileAppsInfoProvider all&#39;elenco dei provider. Il gestore scorre l’elenco di MobileAppsInfoProviders e consente al provider di inserire dati nel file json risultante. L&#39;elenco delle proprietà supportate dal gestore è:

* ***percorso **-**Stringa*** - Percorso di un nodo di istanza dell&#39;app con pge-type=app-instance o un RT che estende /libs/mobileapps/core/components/instance
* ***provider - Stringa*** `[]` - Elenco di MobileAppsInfoProvider completi
* ***targetRootDirectory - String*** - la directory in cui scrivere il file MobileAppsConfig.json.
* **nomeFile - Stringa** - nome facoltativo del file in cui scrivere il JSON; impostazione predefinita: MobileAppsConfig.json

È possibile configurare più gestori mobileappconfig ciascuno con un set univoco di provider che scrivono in file JSON diversi.

### Verifica dei gestori di sincronizzazione dei contenuti {#testing-content-sync-handlers}

**Passaggi per la verifica dell&#39;integrità** Cancella cache

* Cancella cache
* Eseguire il gestore (cache aggiornata)
* Esegui nuovamente il gestore (la cache non deve essere aggiornata)

**Passaggi per il debug**

* Eseguire la configurazione
* Esportare la configurazione o la revisione sul dispositivo
* Se il rendering non riesce, verifica la presenza di *stili/risorse/libs* mancanti o verifica la presenza di percorsi non validi per *stili/risorse/libs*

**Registrazione** Abilita la registrazione del debug ContentSync tramite le configurazioni del logger OSGI nel pacchetto `com.day.cq.contentsync`. Ciò ti consentirà di tenere traccia dei gestori eseguiti e di verificare se hanno aggiornato la cache e segnalato di averla aggiornata.

## Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e sulle responsabilità di un amministratore e di uno sviluppatore, consulta le risorse seguenti:

* [Authoring per Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Per iniziare a sviluppare app AEM Mobile, fai clic [qui](/help/mobile/getting-started-aem-mobile.md).
