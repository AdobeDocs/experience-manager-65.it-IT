---
title: AEM Livefyre Recipes
seo-title: AEM Livefyre Recipes
description: Istruzioni dettagliate sui casi di utilizzo comuni per Adobe Experience Manager Livefyre.
seo-description: Step-by-step instructions on common use cases for Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
exl-id: 7ccd67a7-9945-48c1-9986-f4eaf0f2b961
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 4%

---

# Ricette AEM Livefyre{#aem-livefyre-recipes}

Istruzioni dettagliate sui casi di utilizzo comuni per Adobe Experience Manager Livefyre.

## Cura gli UGC utilizzando i componenti di AEM Livefyre predefiniti e visualizzarli utilizzando Livefyre Media Wall {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall trasmette contenuti sociali e nativi di Livefyre in un muro sociale in tempo reale. Sono disponibili diversi modi per implementare Media Wall in AEM a seconda del caso d’uso e dei requisiti.

Il pacchetto Livefyre AEM fornisce un’implementazione standard, mentre l’integrazione tradizionale fornisce la possibilità di creare componenti personalizzati Livefyre AEM.

### Integrazione AEM {#aem-integration}

Il pacchetto Livefyre Adobe Experience Manager è disponibile per AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 non sono supportati. Per istruzioni dettagliate, vedi [Integrazione con Livefyre](https://helpx.adobe.com/it/experience-manager/6-4/sites/administering/using/livefyre.html).

Per vedere quali app Livefyre sono supportate, vedi [Matrice di supporto AEM per le app Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementazione tradizionale (per componenti AEM personalizzati) {#traditional-implementation-for-customized-aem-components}

Esistono tre modi per implementare Livefyre in un componente AEM personalizzato o altri CMS come WordPress, Sitecore o DemandWare. Un’integrazione tradizionale di Livefyre è agnostica di CMS.

**Metodo 1: Implementazione di Designer app**

* **Cosa:** Il modo più semplice e veloce per integrare un’app Livefyre. Puoi progettare, configurare e generare un codice di incorporamento JavaScript personalizzato per integrare un’app Media Wall su una pagina in pochi minuti.
* **Come:**  [Creare, visualizzare in anteprima, pubblicare e incorporare un’app Muro di file multimediali](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **Esempio:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Metodo 2: Implementazione SDK**

* **Cosa:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) è la libreria principale che abilita App e Auth in un sito. Definisce il globale *window.Livefyre* oggetto e metodo pubblico unico, *Livefyre.required*, che può essere utilizzato per caricare altre librerie JavaScript Livefyre che consentono di incorporare le app Livefyre e di integrarle con piattaforme User Auth di terze parti.

* **Come**: [Utilizza il pacchetto snello-wallpackage dell’SDK JavaScript per Livefyre](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **Esempio**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Per le personalizzazioni avanzate che utilizzano l&#39;SDK, fai riferimento a [SDK di StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Metodo 3: Implementazione API**

* Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero consumando Livefyre e dati social tramite l’ [API Bootstrap e Stream](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Assicurati di seguire [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand)e [Instagram](https://en.instagram-brand.com/) visualizza le linee guida per la creazione dell’interfaccia utente per UGC.

### Integrazione di Media Wall Authentication {#media-wall-authentication-integration}

Per le integrazioni di Media Wall che richiedono l’autenticazione, fai riferimento a:

* [Personalizzare l’integrazione con Single Sign-On](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) per AEM Identity Management
* [Integrazione di Identity](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) per piattaforme di autenticazione di terze parti

### Panoramica del caso d’uso {#use-case-overview}

In qualità di cliente AEM, voglio curare l’utilizzo di UGC utilizzando i componenti predefiniti di Livefyre AEM e visualizzarli utilizzando Livefyre Media Wall:

Passaggi per l’implementazione:

1. [Guida introduttiva](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Configurare AEM per l’utilizzo di Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Trascinare AEM componente Media Wall sulla pagina](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configura i flussi e aggiungi regole per curare gli UGC e visualizzarli sul componente Media Wall](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html)

Per i video di formazione sullo streaming UGC, vedi [Creazione di flussi di contenuto automatici e ricerca di contenuti social in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Esempi cliente {#customer-examples}

* [Muro di CNN](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [Parete multimediale PGA Tour](https://www.pgatour.com/social-hub.html)

Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero consumando Livefyre e dati social tramite l’ [API Bootstrap e Stream](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Per le app Livefyre che richiedono l’autenticazione, consulta [Integrazione di Identity](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) per piattaforme di autenticazione di terze parti.

* [Parete multimediale PGA Tour](https://www.pgatour.com/social-hub.html)
* [Timeout](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integrare i commenti Livefyre utilizzando i componenti AEM o l’integrazione tradizionale con Livefyre {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### Integrazione AEM {#aem-integration-1}

Il pacchetto Livefyre Adobe Experience Manager è disponibile per AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 non sono supportati. Per istruzioni dettagliate, vedi [Integrazione con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Implementazione tradizionale (per componenti AEM personalizzati) {#traditional-implementation-for-customized-aem-components-1}

Sono disponibili tre modi per implementare Livefyre Comments App in un componente AEM personalizzato o in altri CMS come WordPress, Sitecore o DemandWare. Un’integrazione tradizionale di Livefyre è agnostica di CMS.

**Metodo 1: Implementazione di Designer app**

* **Cosa:** Il modo più semplice e veloce per integrare un’app Livefyre. Puoi progettare, configurare e generare un codice di incorporamento JavaScript personalizzato per integrare un’app Media Wall su una pagina in pochi minuti.
* **Come:** [Creare, visualizzare in anteprima, pubblicare e incorporare un’app commenti](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **Esempio:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Metodo 2: Implementazione SDK**

* **Cosa:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) è la libreria principale che abilita App e Auth in un sito. Definisce il globale *window.Livefyre* oggetto e metodo pubblico unico, *Livefyre.required*, che può essere utilizzato per caricare altre librerie JavaScript Livefyre che consentono di incorporare le app Livefyre e di integrarle con piattaforme User Auth di terze parti.

* **Come:**

   * Creare una raccolta/app utilizzando [CollectionMeta token](https://experienceleague.adobe.com/docs/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * Integrare [App commenti](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/comments/c-comments-integration.html) nei siti che utilizzano la struttura del codice di incorporamento Livefyre.js .

* **Esempio:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Per le personalizzazioni avanzate che utilizzano l’SDK, consulta [SDK di StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Metodo 3: Implementazione API**

* Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero consumando Livefyre e dati social tramite l’ [API Bootstrap e Stream](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Integrazione dell’autenticazione dell’app commenti {#comments-app-authentication-integration}

* [Personalizzare l’integrazione con Single Sign-On](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) per AEM Identity Management
* [Integrazione di Identity](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) per piattaforme di autenticazione di terze parti

### Esempi cliente {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Utilizzare l’integrazione di Livefyre AEM Assets per importare UGC in AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configurazione di Livefyre (per Cura e Rights Management UGC):**

1. [Configurare i flussi e aggiungere regole per la cura di UGC nelle cartelle della libreria di risorse Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html).

   1. Per i video di formazione sullo streaming UGC, vedi [Creazione di flussi di contenuto automatici e ricerca di contenuti social in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Raccolta, organizzazione e gestione di contenuti generati dagli utenti curati nelle cartelle della libreria delle risorse di Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/library/assets/c-assets.html).

   1. Per video di formazione sulla creazione e la gestione delle cartelle nella libreria delle risorse di Livefyre Studio, consulta [Utilizzare le risorse in Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Diritti di richiesta per contenuti generati dagli utenti curati che utilizzano Livefyre Studio](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**Configurazione AEM (per l’importazione di UGC in AEM Assets):**

1. [Guida introduttiva](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Configurare AEM per l’utilizzo di Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importazione di contenuti generati dagli utenti generati dagli utenti generati dagli eventi generati da Livefyre in AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Turismo Australia](https://www.australia.com/en-us)

## Integrare le recensioni di Livefyre utilizzando i componenti AEM o l’integrazione tradizionale con Livefyre {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### Integrazione AEM {#aem-integration-2}

Il pacchetto Livefyre Adobe Experience Manager è disponibile per AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 non sono supportati. Per istruzioni dettagliate, vedi [Integrazione con Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

Il componente Revisioni non è un componente supportato per AEM 6.1. Controlla il [Matrice di supporto AEM per tutte le app Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementazione tradizionale (per componenti AEM personalizzati) {#traditional-implementation-for-customized-aem-components-2}

Esistono due modi per implementare Livefyre Reviews App in un componente AEM personalizzato o altri CMS come WordPress, Sitecore o DemandWare. Un’integrazione tradizionale di Livefyre è agnostica di CMS.

**Metodo 1: Implementazione SDK**

* **Cosa:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) è la libreria principale che abilita App e Auth in un sito. Definisce il globale *window.Livefyre* oggetto e metodo pubblico unico, *Livefyre.required*, che può essere utilizzato per caricare altre librerie JavaScript Livefyre che consentono di incorporare le app Livefyre e di integrarle con piattaforme User Auth di terze parti.

* **Come:**

   * Creare le revisioni [CollectionMeta token](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) per specificare i metadati da memorizzare nell&#39;insieme Reviews.
   * Integrare [App recensioni](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) in Sites utilizzando *Livefyre.js* struttura del codice di incorporamento

* **Esempio:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Per le personalizzazioni avanzate che utilizzano l’SDK, consulta [SDK di StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Metodo 2: Implementazione API**

* Per creare esperienze personalizzate e visualizzazioni di dati, le app Livefyre possono essere create da zero utilizzando Livefyre e dati social tramite l’API Bootstrap e Stream.

È possibile trovare API di valutazione e revisione aggiuntive [qui](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Integrazione dell’autenticazione dell’app commenti {#comments-app-authentication-integration-1}

* [Personalizzare l’integrazione con Single Sign-On](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) per AEM Identity Management
* [Integrazione di Identity](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) per piattaforme di autenticazione di terze parti

### Esempi cliente {#customer-examples-2}

* [Timeout](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [ricette](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)
