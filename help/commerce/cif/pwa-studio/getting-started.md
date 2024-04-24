---
title: Guida introduttiva all’estensione AEM per PWA Studi
description: Scopri come distribuire un progetto PWA Studi di contenuti e Commerce headless AEM.
topics: Commerce
feature: Commerce Integration Framework
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# Guida introduttiva all’estensione AEM per PWA Studi {#getting-started-pwa}

PWA Studi si integra perfettamente con Adobe Commerce tramite GraphQL, fornendo opzioni illimitate per la creazione di vetrine e altre esperienze digitali innovative e coinvolgenti.

I frammenti di contenuto sono parti di contenuto con una struttura predefinita che consente di utilizzarli in modo headless utilizzando GraphQL come API in formati diversi (ad esempio, JSON, Markdown) e renderizzati in modo indipendente. I frammenti di contenuto includono tutti i tipi di dati e i campi necessari affinché GraphQL possa garantire che l’applicazione richieda solo ciò che è disponibile e riceva ciò che è previsto. La flessibilità che forniscono in termini di struttura li rende perfetti per l&#39;utilizzo in più posizioni e su più canali.

L’Editor modello per frammenti di contenuto in Adobe Experience Manager semplifica la progettazione della struttura necessaria. Il problema principale per l’integrazione di Frammenti di contenuto di Adobe Experience Manager (o di qualsiasi altro dato) con l’applicazione PWA Studi è il recupero di dati da più endpoint GraphQL. Il motivo è che, per impostazione predefinita, PWA Studi funziona con un singolo endpoint Adobe Commerce GraphQL.

## Architettura {#architecture}

![Architettura PWA headless](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## Configura PWA Studi {#setup-pwa}

Per configurare la tua app PWA Studi, segui Adobe Commerce [Documentazione di PWA Studi](https://developer.adobe.com/commerce/pwa-studio/tutorials/).

Per collegare PWA Studi all’endpoint GraphQL dell’AEM, puoi utilizzare [Estensione AEM per PWA Studi](https://github.com/adobe/aem-pwa-studio-extensions).

1. Estrarre l’archivio

1. Nell’applicazione PWA Studi, aggiungi l’estensione come dipendenza di sviluppo.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Aggiungi il wrapper Apollo Link all’applicazione PWA Studi. In pwa-root/src/index.js, apporta le seguenti modifiche:

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Ulteriori dettagli sulla personalizzazione del client Apollo sono disponibili in [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. Per estendere il componente Navigazione con una voce Blog, aggiungi i seguenti adattamenti a pwa-root/local-intercept.js:

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   Per ulteriori dettagli sulla personalizzazione del componente Navigazione, consulta [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) e nella [Framework di estensibilità](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) PWA Studio.

1. Il client Apollo prevede che l’endpoint AEM GraphQL sia `<https://pwa-studio/endpoint.js>`. Per mappare l’endpoint a questa posizione, personalizza la configurazione UPWARD dell’applicazione PWA Studi: a. Per `pwa-root/.env`, aggiungi la variabile AEM_CFM_GRAPHQL e adattala in modo che punti all’endpoint GraphQL dei frammenti di contenuto AEM.

   Esempio: AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b. Aggiungi un resolver proxy alla configurazione UPWARD. Un esempio di configurazione UPWARD potrebbe essere simile al seguente:

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## Configurazione AEM {#setup-aem}

Segui la documentazione sui Frammenti di contenuto dell’AEM per impostare un endpoint GraphQL per il progetto AEM. Inoltre, nel progetto AEM, aggiungi le seguenti configurazioni per consentire all’applicazione PWA Studi di accedere all’endpoint GraphQL:

* Adobe di criteri di condivisione risorse tra origini granite (com.adobe.granite.cors.impl.CORSPolicyImpl)

  Imposta il `allowedorigin` al nome host completo dell’applicazione PWA.

  Esempio:  `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Filtro referrer Apache Sling (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

  Imposta la proprietà allow.hosts sul nome host dell’applicazione PWA.

  Esempio: pwa-studio-test-vflyn.local.pwadev

Puoi trovare esempi completi di entrambe le configurazioni qui: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

Per mostrare l’endpoint GraphQL, Adobe ha preparato alcuni modelli e dati di esempio per frammenti di contenuto tramite un pacchetto di contenuti. Questi componenti funzionano insieme ai componenti React forniti con l’estensione PWA Studi.

## Guida all’uso {#how-to-use}

Questa estensione è considerata un’implementazione di esempio di come collegare un’applicazione PWA Studi all’AEM per recuperare ed eseguire il rendering del contenuto tramite GraphQL.

A seconda del caso d’uso, desideri creare modelli di Frammento di contenuto personalizzati, che si traducono in uno schema GraphQL personalizzato utilizzabile dai tuoi componenti React.

Le impostazioni di produzione possono variare in diversi aspetti.

* Puoi avere un singolo endpoint GraphQL federato che combina i dati AEM e Adobe Commerce GraphQL invece di personalizzare il client Apollo.
* L’applicazione PWA Studi può utilizzare direttamente l’URL dell’endpoint GraphQL dell’AEM, senza un proxy con UPWARD. Il proxy può anche essere spostato in un livello diverso (ad esempio, CDN).
* L’approccio più adatto alle tue esigenze dipende inoltre fortemente da come distribuisci l’applicazione PWA Studi all’utente finale.

Questa estensione viene fornita con due esempi.

### Blog {#blog}

Visualizza i post di blog in base ad alcuni modelli di frammenti di contenuto. Contiene inoltre esempi di come configurare il client Apollo per l’utilizzo dell’endpoint GraphQL per l’AEM e di come estendere il componente Navigazione in PWA Studi. Consulta [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) per ulteriori dettagli.

### Arricchimento PDP {#pdp-enrichment}

Consente agli addetti al marketing di arricchire facilmente i PDP con contenuto aggiuntivo gestito come Frammenti di contenuto. Consulta [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) per ulteriori dettagli.
