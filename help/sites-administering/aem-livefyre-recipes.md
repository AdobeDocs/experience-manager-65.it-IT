---
title: Ricette AEM Livefyre
seo-title: Ricette AEM Livefyre
description: Istruzioni dettagliate sui casi di utilizzo comuni per Adobe Experience Manager Livefyre.
seo-description: Istruzioni dettagliate sui casi di utilizzo comuni per Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Ricette AEM Livefyre{#aem-livefyre-recipes}

Istruzioni dettagliate sui casi di utilizzo comuni per Adobe Experience Manager Livefyre.

## Cura UGC utilizzando i componenti standard di Livefyre AEM e la visualizzazione tramite Livefyre Media Wall {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall trasferisce contenuti Livefyre sociali e nativi in un vero e proprio muro sociale. In AEM è possibile implementare Media Wall in diversi modi, a seconda dei casi di utilizzo e dei requisiti.

Il pacchetto AEM Livefyre fornisce un&#39;implementazione out-of-box, mentre l&#39;integrazione tradizionale consente di creare componenti Livefyre AEM personalizzati.

### Integrazione AEM {#aem-integration}

Il pacchetto Livefyre Adobe Experience Manager è disponibile per AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 non sono supportati. Per istruzioni dettagliate, consultate [Integrazione con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Per vedere quali app Livefyre sono supportate, consultate la matrice di supporto di [AEM per le app](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)Livefyre.

### Implementazione tradizionale (per componenti AEM personalizzati) {#traditional-implementation-for-customized-aem-components}

Esistono tre modi per implementare Livefyre in un componente AEM personalizzato o altri CMS come WordPress, Siteore o DemandWare. Un&#39;integrazione Livefyre tradizionale è agnostica di CMS.

**Metodo 1: Implementazione app di Designer**

* **** Cosa: Il modo più semplice e veloce per integrare un&#39;app Livefyre. Potete progettare, configurare e generare un codice da incorporare JavaScript personalizzato per integrare in pochi minuti un&#39;app Media Wall su una pagina.
* **** Procedura:  Creare, [visualizzare in anteprima, pubblicare e incorporare un&#39;app Media Wall](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** Esempio: [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Metodo 2: Implementazione SDK**

* **** Cosa: [Livefyre.js](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) è la libreria di base che abilita App e Auth su un sito. Definisce l&#39;oggetto *window.Livefyre* globale e un singolo metodo pubblico, *Livefyre.request*, che può essere utilizzato per caricare altre librerie JavaScript Livefyre che consentono di incorporare le app Livefyre e di integrarsi con le piattaforme di autenticazione utente di terze parti.

* **Procedura**: [Utilizzate il pacchetto di streaming-wallpackage dell&#39;SDK JavaScript di Livefyre](https://marketing.adobe.com/resources/help/en_US/livefyre/?f=c_media_wall_app&s=c_media_wall_integration)

* **Esempio**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Per le personalizzazioni avanzate che utilizzano l’SDK, consulta [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**Metodo 3: Implementazione API**

* Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero utilizzando i dati Livefyre e social tramite l&#39;API [](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)Bootstrap e Stream.

Accertatevi di seguire le linee guida sulla visualizzazione di [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand)e [Instagram](https://en.instagram-brand.com/) al momento della creazione dell&#39;interfaccia utente per UGC.

### Integrazione dell&#39;autenticazione di Media Wall {#media-wall-authentication-integration}

Per le integrazioni di Media Wall che richiedono l’autenticazione, fate riferimento a:

* [Personalizzazione dell&#39;integrazione](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) con Single Sign On per AEM Identity Management
* [Integrazione](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) delle identità per le piattaforme di autenticazione di terze parti

### Cenni preliminari sull’utilizzo {#use-case-overview}

In qualità di cliente AEM, desidero curare l’utilizzo di UGC con i componenti standard di Livefyre AEM e visualizzarlo tramite Livefyre Media Wall:

Passaggi per l&#39;implementazione:

1. [Introduzione](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Configurare AEM per l&#39;utilizzo di Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Trascinare il componente AEM Media Wall sulla pagina](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configurare i flussi e aggiungere regole per la cura dell’UGC e la visualizzazione sul componente Media Wall](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)

Per video di formazione sullo streaming UGC, consultate [Creare flussi di contenuto automatici e cercare contenuti social in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Esempi di clienti {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)

Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero utilizzando i dati Livefyre e social tramite l&#39;API [](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)Bootstrap e Stream.

Per le app Livefyre che richiedono l&#39;autenticazione, vedete Integrazione [](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) identità per le piattaforme di autenticazione di terze parti.

* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)
* [Timeout](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integrare i commenti Livefyre utilizzando i componenti AEM o l&#39;integrazione Livefyre tradizionale {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### Integrazione AEM {#aem-integration-1}

Il pacchetto Livefyre Adobe Experience Manager è disponibile per AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 non sono supportati. Per istruzioni dettagliate, consultate [Integrazione con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Implementazione tradizionale (per componenti AEM personalizzati) {#traditional-implementation-for-customized-aem-components-1}

Esistono tre modi per implementare l’app dei commenti Livefyre in un componente AEM personalizzato o in altri CMS come WordPress, Siteore o DemandWare. Un&#39;integrazione Livefyre tradizionale è agnostica di CMS.

**Metodo 1: Implementazione app di Designer**

* **** Cosa: Il modo più semplice e veloce per integrare un&#39;app Livefyre. Potete progettare, configurare e generare un codice da incorporare JavaScript personalizzato per integrare in pochi minuti un&#39;app Media Wall su una pagina.
* **** Procedura: Creare, [visualizzare in anteprima, pubblicare e incorporare un&#39;app per commenti](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** Esempio: [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Metodo 2: Implementazione SDK**

* **** Cosa: [Livefyre.js](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) è la libreria di base che abilita App e Auth su un sito. Definisce l&#39;oggetto *window.Livefyre* globale e un singolo metodo pubblico, *Livefyre.request*, che può essere utilizzato per caricare altre librerie JavaScript Livefyre che consentono di incorporare le app Livefyre e di integrarsi con le piattaforme di autenticazione utente di terze parti.

* **Procedura:**

   * Create una raccolta/app utilizzando il token [CollectionMeta](https://marketing.adobe.com/resources/help/en_US/livefyre/t_create_a_collectionmeta_token.html).
   * Integrare l&#39;app [dei](https://marketing.adobe.com/resources/help/en_US/livefyre/c_comments_integration.html) commenti nei siti utilizzando la struttura del codice da incorporare di Livefyre.js.

* **** Esempio: [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Per le personalizzazioni avanzate che utilizzano l’SDK, consulta SDK [StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Metodo 3: Implementazione API**

* Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero utilizzando i dati Livefyre e social tramite l&#39;API [](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)Bootstrap e Stream.

### Integrazione autenticazione app commenti {#comments-app-authentication-integration}

* [Personalizzazione dell&#39;integrazione](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) con Single Sign On per AEM Identity Management
* [Integrazione](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) delle identità per le piattaforme di autenticazione di terze parti

### Esempi di clienti {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Utilizzare l’integrazione di Livefyre AEM Assets per importare contenuti UGC in AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configurazione Livefyre (per Cura UGC e Rights Management):**

1. [Configura flussi e aggiungi regole per curare i contenuti UGC nelle cartelle](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)della libreria di risorse Livefyre.

   1. Per video di formazione sullo streaming UGC, consultate [Creare flussi di contenuto automatici e cercare contenuti social in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Raccogliete, organizzate e gestite contenuti UGC specifici nelle cartelle](https://marketing.adobe.com/resources/help/en_US/livefyre/c_assets.html)Libreria risorse Livefyre.

   1. Per video di formazione sulla creazione e gestione di cartelle nella Libreria risorse di Livefyre Studio, consultate [Operazioni con le risorse in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Richiedi diritti per UGC curato tramite Livefyre Studio](https://marketing.adobe.com/resources/help/en_US/livefyre/c_how_requesting_rights_works.html).

**Impostazione AEM (per importare UGC in AEM Assets):**

1. [Introduzione](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Configurare AEM per l&#39;utilizzo di Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importazione di contenuti generati dagli utenti generati da Livefyre in AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Tourism Australia](https://www.australia.com/en-us)

## Integrare le recensioni di Livefyre utilizzando i componenti di AEM o la tradizionale integrazione con Livefyre {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### Integrazione AEM {#aem-integration-2}

Il pacchetto Livefyre Adobe Experience Manager è disponibile per AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 non sono supportati. Per istruzioni dettagliate, consultate [Integrazione con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Il componente Recensioni non è un componente supportato per AEM 6.1. Controlla la matrice di supporto di [AEM per tutte le app](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)Livefyre.

### Implementazione tradizionale (per componenti AEM personalizzati) {#traditional-implementation-for-customized-aem-components-2}

Esistono due modi per implementare Livefyre Reviews App in un componente AEM personalizzato o altri CMS come WordPress, Sitecore o DemandWare. Un&#39;integrazione Livefyre tradizionale è agnostica di CMS.

**Metodo 1: Implementazione SDK**

* **** Cosa: [Livefyre.js](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) è la libreria di base che abilita App e Auth su un sito. Definisce l&#39;oggetto *window.Livefyre* globale e un singolo metodo pubblico, *Livefyre.request*, che può essere utilizzato per caricare altre librerie JavaScript Livefyre che consentono di incorporare le app Livefyre e di integrarsi con le piattaforme di autenticazione utente di terze parti.

* **Procedura:**

   * Create il token [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) CollectionMeta di recensioni per specificare i metadati da memorizzare nella raccolta Reviews.
   * Integrare l&#39;app [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) Reviews nei siti tramite la struttura del codice da incorporare di *Livefyre.js*

* **** Esempio:  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Per le personalizzazioni avanzate che utilizzano l’SDK, consulta SDK [StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Metodo 2: Implementazione API**

* Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero utilizzando i dati Livefyre e social tramite l&#39;API Bootstrap e Stream.

Ulteriori valutazioni e recensioni API sono disponibili [qui](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Integrazione autenticazione app commenti {#comments-app-authentication-integration-1}

* [Personalizzazione dell&#39;integrazione](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) con Single Sign On per AEM Identity Management
* [Integrazione](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) delle identità per le piattaforme di autenticazione di terze parti

### Esempi di clienti {#customer-examples-2}

* [Timeout](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

