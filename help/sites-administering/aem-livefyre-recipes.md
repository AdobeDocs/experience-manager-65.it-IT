---
title: AEM Ricette Livefyre
seo-title: AEM Ricette Livefyre
description: Istruzioni dettagliate sui casi di utilizzo comuni per Adobe Experience Manager Livefyre.
seo-description: Istruzioni dettagliate sui casi di utilizzo comuni per Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 072898f18d418eac8e9d9e94453db34d62dd3ed9
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 2%

---


# AEM Livefyre Recipes{#aem-livefyre-recipes}

Istruzioni dettagliate sui casi di utilizzo comuni per Adobe Experience Manager Livefyre.

## Cura UGC utilizzando i componenti integrati di AEM Livefyre e visualizzi tramite Livefyre Media Wall {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall trasferisce contenuti Livefyre sociali e nativi in un vero e proprio muro sociale. A seconda dei casi d’uso e dei requisiti, in AEM è possibile implementare Media Wall in diversi modi.

Il pacchetto AEM Livefyre fornisce un&#39;implementazione out-of-box, mentre l&#39;integrazione tradizionale consente di creare componenti Livefyre AEM personalizzati.

### Integrazione AEM {#aem-integration}

Il pacchetto Adobe Experience Manager Livefyre è disponibile per AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 non sono supportati. Per istruzioni dettagliate, consultate [Integrazione con Livefyre](https://helpx.adobe.com/it/experience-manager/6-4/sites/administering/using/livefyre.html).

Per vedere quali app Livefyre sono supportate, consultate la [AEM matrice di supporto per le app Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementazione tradizionale (per componenti AEM personalizzati) {#traditional-implementation-for-customized-aem-components}

Esistono tre modi per implementare Livefyre in un componente AEM personalizzato o altri CMS come WordPress, Sitecore o DemandWare. Un&#39;integrazione Livefyre tradizionale è agnostica di CMS.

**Metodo 1: Implementazione app di Designer**

* **Cosa:** Metodo più semplice e veloce per integrare un&#39;app Livefyre. Potete progettare, configurare e generare un codice da incorporare JavaScript personalizzato per integrare in pochi minuti un&#39;app Media Wall su una pagina.
* **Come:**  [creare, visualizzare in anteprima, pubblicare e incorporare un’app per muri di file multimediali](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Esempio:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Metodo 2: Implementazione SDK**

* **What:** [Livefyre.](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) jsis la libreria di base che abilita App e Auth su un sito. Definisce l&#39;oggetto *window.Livefyre* globale e un singolo metodo pubblico, *Livefyre.request*, che può essere utilizzato per caricare altre librerie JavaScript Livefyre che consentono di incorporare le app Livefyre e di integrarsi con le piattaforme di autenticazione utente di terze parti.

* **Procedura**:  [Utilizzate il pacchetto di streaming-wallpackage dell&#39;SDK JavaScript di Livefyre](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **Esempio**:  [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Per le personalizzazioni avanzate che utilizzano l&#39;SDK, fare riferimento a [SDK StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Metodo 3: Implementazione API**

* Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero utilizzando i dati Livefyre e social tramite l&#39;API [Bootstrap e Stream](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Quando create l&#39;interfaccia per UGC, accertatevi di seguire le [linee guida di visualizzazione di &lt;a0/>Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand) e [Instagram](https://en.instagram-brand.com/).

### Integrazione autenticazione di Media Wall {#media-wall-authentication-integration}

Per le integrazioni di Media Wall che richiedono l’autenticazione, fate riferimento a:

* [Personalizza Single Sign On ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) Integrationper AEM Identity Management
* [Integrazione ](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) delle identità per le piattaforme di autenticazione di terze parti

### Cenni preliminari sull&#39;utilizzo dei casi {#use-case-overview}

In qualità di cliente AEM, desidero curare l’UGC utilizzando i componenti AEM integrati di Livefyre e visualizzarlo tramite Livefyre Media Wall:

Passaggi per l&#39;implementazione:

1. [Guida introduttiva](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Configurare AEM per l&#39;utilizzo di Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Trascinare AEM componente Media Wall sulla pagina](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configurare i flussi e aggiungere regole per la cura dell’UGC e la visualizzazione sul componente Media Wall](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)

Per i video di formazione sullo streaming UGC, consultate [Create Automatic Content Streams and Search Social Content in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html) (Creazione di flussi di contenuto automatici e ricerca di contenuti social network in Livefyre).

### Esempi cliente {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)

Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero utilizzando i dati Livefyre e social tramite l&#39;API [Bootstrap e Stream](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Per le app Livefyre che richiedono l&#39;autenticazione, consultate [Integrazione identità](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) per le piattaforme di autenticazione di terze parti.

* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)
* [Timeout](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integrare i commenti Livefyre utilizzando i componenti AEM o l&#39;integrazione Livefyre tradizionale {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### Integrazione AEM {#aem-integration-1}

Il pacchetto Adobe Experience Manager Livefyre è disponibile per AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 non sono supportati. Per istruzioni dettagliate, consultate [Integrazione con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Implementazione tradizionale (per componenti AEM personalizzati) {#traditional-implementation-for-customized-aem-components-1}

Esistono tre modi per implementare l&#39;app dei commenti Livefyre in un componente AEM personalizzato o in altri CMS come WordPress, Siteore o DemandWare. Un&#39;integrazione Livefyre tradizionale è agnostica di CMS.

**Metodo 1: Implementazione app di Designer**

* **Cosa:** Metodo più semplice e veloce per integrare un&#39;app Livefyre. Potete progettare, configurare e generare un codice da incorporare JavaScript personalizzato per integrare in pochi minuti un&#39;app Media Wall su una pagina.
* **Come:** [creare, visualizzare in anteprima, pubblicare e incorporare un&#39;app per commenti](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Esempio:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Metodo 2: Implementazione SDK**

* **What:** [Livefyre.](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) jsis la libreria di base che abilita App e Auth su un sito. Definisce l&#39;oggetto *window.Livefyre* globale e un singolo metodo pubblico, *Livefyre.request*, che può essere utilizzato per caricare altre librerie JavaScript Livefyre che consentono di incorporare le app Livefyre e di integrarsi con le piattaforme di autenticazione utente di terze parti.

* **Procedura:**

   * Create una raccolta/app utilizzando [CollectionMeta token](https://docs.adobe.com/content/help/en/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * Integrare [Comments App](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/comments/c-comments-integration.html) nei siti utilizzando la struttura del codice da incorporare di Livefyre.js.

* **Esempio:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Per le personalizzazioni avanzate che utilizzano l&#39;SDK, vedi [SDK StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Metodo 3: Implementazione API**

* Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero utilizzando i dati Livefyre e social tramite l&#39;API [Bootstrap e Stream](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Integrazione autenticazione app commenti {#comments-app-authentication-integration}

* [Personalizza Single Sign On ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) Integrationper AEM Identity Management
* [Integrazione ](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) delle identità per le piattaforme di autenticazione di terze parti

### Esempi cliente {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Utilizzate l&#39;integrazione Livefyre  AEM Assets per importare UGC in  AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configurazione Livefyre (per cura e Rights Management UGC):**

1. [Configura flussi e aggiungi regole per curare i contenuti UGC nelle cartelle](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html) della libreria di risorse Livefyre.

   1. Per i video di formazione sullo streaming UGC, consultate [Create Automatic Content Streams and Search Social Content in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html) (Creazione di flussi di contenuto automatici e ricerca di contenuti social network in Livefyre).

1. [Raccogliete, organizzate e gestite contenuti UGC specifici nelle cartelle](https://docs.adobe.com/content/help/en/livefyre/using/library/assets/c-assets.html) Libreria risorse Livefyre.

   1. Per video di formazione sulla creazione e gestione di cartelle nella Libreria risorse di Livefyre Studio, consultate [Operazioni con le risorse in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Richiedi diritti per UGC curato tramite Livefyre Studio](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**Impostazione AEM (per importare UGC in  AEM Assets):**

1. [Guida introduttiva](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Configurare AEM per l&#39;utilizzo di Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importa UGC curato da Livefyre in  AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Tourism Australia](https://www.australia.com/en-us)

## Integrare le recensioni di Livefyre utilizzando i componenti AEM o l&#39;integrazione tradizionale di Livefyre {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### Integrazione AEM {#aem-integration-2}

Il pacchetto Adobe Experience Manager Livefyre è disponibile per AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 non sono supportati. Per istruzioni dettagliate, consultate [Integrazione con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Il componente Recensioni non è un componente supportato per AEM 6.1. Controllare la [AEM matrice di supporto per tutte le app Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementazione tradizionale (per componenti AEM personalizzati) {#traditional-implementation-for-customized-aem-components-2}

Esistono due modi per implementare Livefyre Reviews App in un componente AEM personalizzato o altri CMS come WordPress, Sitecore o DemandWare. Un&#39;integrazione Livefyre tradizionale è agnostica di CMS.

**Metodo 1: Implementazione SDK**

* **What:** [Livefyre.](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) jsis la libreria di base che abilita App e Auth su un sito. Definisce l&#39;oggetto *window.Livefyre* globale e un singolo metodo pubblico, *Livefyre.request*, che può essere utilizzato per caricare altre librerie JavaScript Livefyre che consentono di incorporare le app Livefyre e di integrarsi con le piattaforme di autenticazione utente di terze parti.

* **Procedura:**

   * Create le Recensioni [CollectionMeta token](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) per specificare i metadati da memorizzare nella raccolta Reviews.
   * Integrare [Recensioni di app](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) nei siti mediante la struttura del codice da incorporare *Livefyre.js*

* **Esempio:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Per le personalizzazioni avanzate che utilizzano l&#39;SDK, vedi [SDK StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Metodo 2: Implementazione API**

* Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero utilizzando i dati Livefyre e social tramite l&#39;API Bootstrap e Stream.

Ulteriori valutazioni e recensioni API sono disponibili [qui](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Integrazione autenticazione app commenti {#comments-app-authentication-integration-1}

* [Personalizza Single Sign On ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) Integrationper AEM Identity Management
* [Integrazione ](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) delle identità per le piattaforme di autenticazione di terze parti

### Esempi cliente {#customer-examples-2}

* [Timeout](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

