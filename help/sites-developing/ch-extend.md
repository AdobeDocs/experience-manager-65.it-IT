---
title: Estensione di ContextHub
description: Definisci nuovi tipi di store e moduli ContextHub quando quelli forniti non soddisfano i requisiti della soluzione
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Estensione di ContextHub{#extending-contexthub}

Definisci nuovi tipi di store e moduli ContextHub quando quelli forniti non soddisfano i requisiti della soluzione.

## Creazione di candidati per store personalizzati {#creating-custom-store-candidates}

Gli store ContextHub vengono creati dai candidati di store registrati. Per creare un archivio personalizzato, crea e registra un candidato per lo store.

Il file JavaScript che include il codice che crea e registra il candidato per l’archivio deve essere incluso in un [cartella della libreria client](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoria della cartella deve corrispondere al seguente pattern:

```xml
contexthub.store.[storeType]
```

Il `[storeType]` parte della categoria è il `storeType` con cui è registrato il candidato del punto vendita. (vedere [Registrazione di un candidato per l’archivio ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Ad esempio, per storeType di `contexthub.mystore`, la categoria della cartella della libreria client deve essere `contexthub.store.contexthub.mystore`.

### Creazione di un candidato per l’archivio ContextHub {#creating-a-contexthub-store-candidate}

Per creare un candidato per lo store, utilizzare [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) funzione per estendere uno degli archivi di base:

* [&quot;ContextHub.Store.PersistedStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&quot;ContextHub.Store.SessionStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&quot;ContextHub.Store.JSONPStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&quot;ContextHub.Store.PersistedJSONPStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Ogni base store estende [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) archiviare.

L&#39;esempio seguente crea l&#39;estensione più semplice del `ContextHub.Store.PersistedStore` candidato store:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

Realisticamente, i candidati all’archivio personalizzato definiscono funzioni aggiuntive o sovrascrivono la configurazione iniziale dell’archivio. Diversi [candidati per l&#39;archivio esempi](/help/sites-developing/ch-samplestores.md) sono installati nel repository seguente `/libs/granite/contexthub/components/stores`. Per apprendere da questi esempi, utilizza CRXDE Liti per aprire i file JavaScript.

### Registrazione di un candidato per l’archivio ContextHub {#registering-a-contexthub-store-candidate}

Registra un candidato per store per integrarlo con il framework ContextHub e consentirne la creazione. Per registrare un candidato per lo store, utilizzare [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) funzione del `ContextHub.Utils.storeCandidates` classe.

Quando si registra un candidato per un punto vendita, è necessario specificare un nome per il tipo di punto vendita. Quando si crea un archivio dal candidato, si utilizza il tipo di archivio per identificare il candidato su cui si basa.

Quando si registra un candidato per lo store, si indica la sua priorità. Quando un candidato per lo store viene registrato utilizzando lo stesso tipo di store di un candidato per lo store già registrato, viene utilizzato il candidato con la priorità più elevata. Pertanto, puoi sostituire i candidati store esistenti con nuove implementazioni.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Di solito è necessario un solo candidato e la priorità può essere impostata su `0`. Ma se sei interessato, puoi scoprire di più [registrazioni più avanzate,](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) che consente di scegliere una delle poche implementazioni dello store in base alla condizione JavaScript (`applies`) e priorità del candidato.

## Creazione di tipi di moduli dell’interfaccia utente ContextHub {#creating-contexthub-ui-module-types}

Creare tipi di moduli dell’interfaccia utente personalizzati quando [installato con ContextHub](/help/sites-developing/ch-samplemodules.md) non soddisfa le tue esigenze. Per creare un tipo di modulo UI, crea un modulo di rendering dell’interfaccia utente estendendo il `ContextHub.UI.BaseModuleRenderer` e quindi registrarlo con `ContextHub.UI`.

Per creare un modulo di rendering dell’interfaccia utente, crea un `Class` oggetto contenente la logica per il rendering del modulo dell’interfaccia utente. Come minimo, la classe deve eseguire le azioni seguenti:

* Estendi il `ContextHub.UI.BaseModuleRenderer` classe. Questa classe è l’implementazione di base per tutti i renderer dei moduli di interfaccia utente. Il `Class` l&#39;oggetto definisce una proprietà denominata `extend` che si utilizza per denominare questa classe come quella che viene estesa.

* Fornisci una configurazione predefinita. Creare un `defaultConfig` proprietà. Questa proprietà è un oggetto che include le proprietà definite per [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) e tutte le altre proprietà necessarie.

Origine per `ContextHub.UI.BaseModuleRenderer` si trova in /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js. Per registrare il renderer, utilizzare [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) metodo del `ContextHub.UI` classe. Specifica un nome per il tipo di modulo. Quando gli amministratori creano un modulo di interfaccia utente basato su questo renderer, specificano questo nome.

Crea e registra la classe renderer in una funzione anonima a esecuzione automatica. L’esempio seguente è basato sul codice sorgente del modulo dell’interfaccia utente contexthub.browserinfo. Questo modulo di interfaccia utente è una semplice estensione del `ContextHub.UI.BaseModuleRenderer` classe.

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

Il file JavaScript che include il codice che crea e registra il renderer deve essere incluso in un [cartella della libreria client](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoria della cartella deve corrispondere al seguente pattern:

```xml
contexthub.module.[moduleType]
```

Il `[moduleType]` parte della categoria è il `moduleType` con cui è registrato il modulo di rendering. Ad esempio, per `moduleType` di `contexthub.browserinfo`, la categoria della cartella della libreria client deve essere `contexthub.module.contexthub.browserinfo`.
