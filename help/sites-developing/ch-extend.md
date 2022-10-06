---
title: Estensione di ContextHub
seo-title: Extending ContextHub
description: Definire nuovi tipi di archivi e moduli ContextHub quando quelli forniti non soddisfano i requisiti della soluzione
seo-description: Define new types of ContextHub stores and modules when the ones provided do not meet your solution requirements
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# Estensione di ContextHub{#extending-contexthub}

Definisci nuovi tipi di archivi e moduli ContextHub quando quelli forniti non soddisfano i requisiti della soluzione.

## Creazione di candidati store personalizzati {#creating-custom-store-candidates}

Gli archivi ContextHub vengono creati dai candidati store registrati. Per creare uno store personalizzato, è necessario creare e registrare un candidato allo store.

Il file javascript che include il codice che crea e registra il candidato store deve essere incluso in un [cartella libreria client](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoria della cartella deve corrispondere al seguente pattern:

```xml
contexthub.store.[storeType]
```

La `[storeType]` parte della categoria è `storeType` con cui è registrato il candidato del negozio. (Vedi [Registrazione di un candidato all’archivio ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Ad esempio, per storeType di `contexthub.mystore`, la categoria della cartella della libreria client deve essere `contexthub.store.contexthub.mystore`.

### Creazione di un candidato all’archivio ContextHub {#creating-a-contexthub-store-candidate}

Per creare un candidato allo store, utilizza la [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) funzione per estendere uno degli archivi di base:

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Tieni presente che ogni archivio di base estende [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) archiviare.

Nell&#39;esempio seguente viene creata l&#39;estensione più semplice di `ContextHub.Store.PersistedStore` candidato al negozio:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

In modo realistico, i candidati all&#39;archivio personalizzati definiranno funzioni aggiuntive o ignoreranno la configurazione iniziale dell&#39;archivio. Diversi [candidati allo store di esempio](/help/sites-developing/ch-samplestores.md) sono installati nell&#39;archivio sottostante `/libs/granite/contexthub/components/stores`. Per imparare da questi esempi, utilizza CRXDE Lite per aprire i file javascript.

### Registrazione di un candidato all’archivio ContextHub {#registering-a-contexthub-store-candidate}

Registra un candidato store per integrarlo con il framework ContextHub e abilita la creazione di archivi da esso. Per registrare un candidato di un negozio, utilizza la [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) funzione `ContextHub.Utils.storeCandidates` classe.

Quando si registra un candidato allo store, specificare un nome per il tipo di store. Quando si crea un negozio dal candidato, si utilizza il tipo di negozio per identificare il candidato su cui si basa.

Quando si registra un candidato al negozio, viene indicata la sua priorità. Quando un candidato viene registrato utilizzando lo stesso tipo di negozio di un candidato già registrato, viene utilizzato il candidato con la priorità più alta. Pertanto, puoi sostituire i candidati esistenti allo store con nuove implementazioni.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Nella maggior parte dei casi è necessario un solo candidato e la priorità può essere impostata su `0`, ma se siete interessati potete saperne di più [registrazioni più avanzate,](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) che consente di scegliere una delle poche implementazioni store in base alla condizione javascript (`applies`) e priorità del candidato.

## Creazione di tipi di moduli di interfaccia utente ContextHub {#creating-contexthub-ui-module-types}

Crea tipi di moduli di interfaccia utente personalizzati quando quelli che sono [installato con ContextHub](/help/sites-developing/ch-samplemodules.md) non soddisfa le tue esigenze. Per creare un tipo di modulo dell’interfaccia utente, crea un nuovo modulo di rendering dell’interfaccia utente estendendo `ContextHub.UI.BaseModuleRenderer` e quindi registrarla con `ContextHub.UI`.

Per creare un modulo di rendering dell’interfaccia utente, crea un `Class` oggetto contenente la logica che esegue il rendering del modulo dell’interfaccia utente. Come minimo, la classe deve eseguire le azioni seguenti:

* Estendi la `ContextHub.UI.BaseModuleRenderer` classe. Questa classe è l’implementazione di base per tutti i moduli di rendering dell’interfaccia utente. La `Class` l&#39;oggetto definisce una proprietà denominata `extend` che si utilizza per denominare questa classe come quella in corso di estensione.

* Fornisci una configurazione predefinita. Crea un `defaultConfig` proprietà. Questa proprietà è un oggetto che include le proprietà definite per [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) Modulo dell’interfaccia utente e tutte le altre proprietà richieste.

L&#39;origine per `ContextHub.UI.BaseModuleRenderer` si trova in /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.  Per registrare il modulo di rendering, utilizza la [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) metodo `ContextHub.UI` classe. È necessario specificare un nome per il tipo di modulo. Quando gli amministratori creano un modulo di interfaccia utente basato su questo modulo di rendering, specificano questo nome.

Crea e registra la classe renderer in una funzione anonima con esecuzione automatica. L’esempio seguente è basato sul codice sorgente per il modulo dell’interfaccia utente contexthub.browserinfo. Questo modulo di interfaccia utente è una semplice estensione del `ContextHub.UI.BaseModuleRenderer` classe.

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

Il file javascript che include il codice che crea e registra il renderer deve essere incluso in un [cartella libreria client](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoria della cartella deve corrispondere al seguente pattern:

```xml
contexthub.module.[moduleType]
```

La `[moduleType]` parte della categoria è `moduleType` con cui viene registrato il modulo di rendering. Ad esempio, per `moduleType` di `contexthub.browserinfo`, la categoria della cartella della libreria client deve essere `contexthub.module.contexthub.browserinfo`.
